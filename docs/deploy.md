# Deploy — 2021.trondheimdc.no

A static archive of TDC Community Week 2021. There is no app server, no database and no secret on the server.

```text
push to main
    → GitHub Actions: stage web files, rsync → /var/www/sites/2021.trondheimdc.no/public
```

| Part | Value |
|---|---|
| Public URL | https://2021.trondheimdc.no |
| Static files | `/var/www/sites/2021.trondheimdc.no/public` |
| Nginx config | [nginx-2021.trondheimdc.no.conf](./nginx-2021.trondheimdc.no.conf) |
| Nginx logs | `/var/www/sites/2021.trondheimdc.no/logs/` |
| Workflow | `.github/workflows/cd.yml` (push to `main`, or run by hand) |

## 1. DNS (one-time)

`2021.trondheimdc.no` must be a CNAME to `worldwide.trondheimdc.no`. Today it is a CNAME to `connect.trondheimdc.no`, which is the old server. Change it, and do it before step 2, because certbot's HTTP challenge needs the name to resolve to worldwide.

There is no wildcard for `*.trondheimdc.no`. Each name needs its own record.

## 2. GitHub (one-time)

| Type | Name | Value |
|---|---|---|
| Secret | `SSH_HOST` / `SSH_USER` / `SSH_PRIVATE_KEY` | Same as the other sites (org secrets) |

`SSH_USER` must be able to write to the static files directory below. The repo must have access to the org secrets.

## 3. Server (one-time)

```bash
# From your machine
scp docs/setup-server.sh docs/nginx-2021.trondheimdc.no.conf <server>:
# On the server, with the user behind the SSH_USER secret
sudo bash setup-server.sh <deploy-user>
```

[setup-server.sh](./setup-server.sh) creates the site and log directories, gets the certificate from certbot (webroot, port 80 only until it exists), then installs the full nginx config and reloads. It is safe to run again.

## 4. First deploy

Push `main`, or run **Actions → CD - Deploy** by hand (`workflow_dispatch`).

## 5. Verify after deploy

```bash
curl -sI https://2021.trondheimdc.no | head -1                    # 200
curl -sI https://2021.trondheimdc.no/css/app.css | head -1        # 200
curl -sI https://2021.trondheimdc.no/finnes-ikke | head -1        # 404
curl -sI http://2021.trondheimdc.no | grep -i ^location           # → https://
```

Then open the site in a browser with the dev tools console open. A Content-Security-Policy violation there means something new loads from another origin, and the policy in the nginx config needs to allow it.
