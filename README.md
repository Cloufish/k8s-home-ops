<div align="center">

## My Home Operations repository

_... managed by Flux, and GitHub Actions_ :robot:


</div>
<br>
This repository is meant for me to configure and manage my cluster.
And to learn more K8s concepts and GitOps, DevOps 
I'll try to create my own [Helm Charts](https://github.com/Cloufish/helm-charts)

### INFRASTRUCTURE 
<table>
    <tr>
        <th>Logo</th>
        <th>Name</th>
        <th>Description</th>
    </tr>
    <tr>
        <td><img width="32" src="https://cdn.jsdelivr.net/gh/walkxcode/dashboard-icons/svg/cert-manager.svg"></td>
        <td><a href="https://cert-manager.io/">Cert Manager</a></td>
        <td>X.509 certificate management for Kubernetes.</td>
    </tr>
    <tr>
        <td><img width="32" src="https://raw.githubusercontent.com/flannel-io/flannel/refs/heads/master/logos/flannel-glyph-color.png"></td>
        <td><a href="https://github.com/flannel-io/flannel">Flannel</a></td>
        <td>My CNI of choice, used on all clusters</td>
    </tr>
    <tr>
        <td><img width="32" src="https://cdn.jsdelivr.net/gh/walkxcode/dashboard-icons/png/cloudflare-zero-trust.png"></td>
        <td><a href="https://developers.cloudflare.com/cloudflare-one/">Cloudflare Zero Trust</a></td>
        <td>Used for private tunnels to expose public services (without requiring a public IP).</td>
    </tr>
    <tr>
        <td><img width="32" src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/postgresql.svg"></td>
        <td><a href="https://cloudnative-pg.io/">CloudNativePG</a></td>
        <td>Database operator for running PostgreSQL clusters</td>
    </tr>
    <tr>
        <td><img width="32" src="https://getsops.io/favicons/favicon.ico"></td>
        <td><a href="https://getsops.io/">SOPS and AGE Encryption</a></td>
        <td>Used to encrypt secrets used by this repository</td>
    </tr>
    <tr>
        <td><img width="32" src="https://cdn.jsdelivr.net/gh/homarr-labs/dashboard-icons/svg/flux-cd.svg"></td>
        <td><a href="https://fluxcd.io/">Flux CD</a></td>
        <td>My GitOps solution of choice. For K8s Administrator it's better than ArgoCD.</td>
    </tr>
    <tr>
        <td><img width="32" src="https://prometheus-operator.dev/favicon.svg"></td>
        <td><a href="https://prometheus-operator.dev/">Prometheus Operator</a></td>
        <td>Manages deploying Prometheus, Grafana, AlertManager in my cluster</td>
    </tr>
    <tr>
        <td><img width="32" src="https://www.svgrepo.com/download/374041/renovate.svg"></td>
        <td><a href="https://github.com/renovatebot/renovate">Renovate</a></td>
        <td>Automated dependency updates.</td>
    </tr>
    <tr>
        <td><img width="32" src="https://github.com/longhorn/website/blob/master/static/img/logos/longhorn-stacked-color.png"></td>
        <td><a href="https://longhorn.io/">Longhorn</a></td>
        <td>A distributed block storage system for Kubernetes with built-in Backups and Snapshots mechanism</td>
    </tr>
</table>

### STEPS TO DEPLOY NEW APPLICATION
1. Define `${APP_app_name}` variable in `clusters/production/apps.yaml` in `postBuild.substitute`
2. Copy the existing application implementation in `apps/base/APP` and `apps/base/production` (OR `apps/base/staging`)
3. Change name of variables inside `release.yaml` by highlighting APP keyword and using shortcut Ctrl + Shift + L 

### STEPS TO DEPLOY NEW INFRASTRUCTURE APPLICATION/CONTROLLER
- When deploying infrastructure app there's no distinction between production and staging.  

1. You define your HelmRelease inside `infrastructure/controllers/release.yaml`  
2.  You need to add a resource to your release.yaml inside `infrastructure/controllers/kustomization.yaml`  
3. Additional Resources need to be inside `infrastructure/configs/` and also need to be added to `infrastructure/configs/kustomization.yaml`

### HOW TO DECRYPT, ENCRYPT SECRETS WITH SOPS AND AGE
1. Proceed with the initial guide https://fluxcd.io/flux/guides/mozilla-sops/
> Following instructions will be for WSL. If you are working on Linux then it's better to use VSCode Extension for SOPS. However VSCode installed on Windows didn't detect sops in WSL environment, and also on Windows 
2. Put your generated keys with `age` inside default folder for sops keys, which is `$HOME/.config/sops/age/age.agekey`
3. Configure config file for `.sops.yaml` (Already in the repository). Put there your **public** `age` key
4. In your `$HOME/.bashrc` set `export SOPS_AGE_KEY_FILE="/home/cloufish/.config/sops/age/age.agekey"` 
5. Use `sops decrypt secrets.yaml --output=secrets.yaml` or `sops encrypt secrets.yaml --output=secrets.yaml`
6. However, **even better option** is to use VSCode Extension to automatically (This is tricky in Windows environment)

### TODO: 
- [ ] **Renovate**
 -[X] longhorn
- [ ] Vaultwarden 
- [ ] Uptime Kuma
- [X] Grafana
- [X] Prometheus 
- [X] Alert Manager
- [ ] Loki with Grafana-Operator
- [ ] **OAuth 2.0 for Code Server** 
- [ ] **MFA with Authelia for Code Server**
- [ ] languagetool 
- [ ] Blocky DNS Server
- [ ] Searxng 
- [ ] Compozerize 
- [ ] DSOMM 
- [ ] Devdocs
- [ ] Home Assistant
- [ ] n8n
- [ ] pgadmin
- [ ] commafeed
- [ ] ReadLater
- [ ] ChatGPT Frontend
- [ ] Lidify
