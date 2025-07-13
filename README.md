<div align="center">

## My Home Operations repository

_... managed by Flux, and GitHub Actions_ :robot:


</div>
<br>
This repository is meant for me to configure and manage my cluster.
And to learn more K8s concepts and GitOps, DevOps 
I'll try to create my own [Helm Charts](https://github.com/Cloufish/helm-charts)

## STEPS TO DEPLOY NEW APPLICATION
1. Define `${APP_app_name}` variable in `clusters/production/apps.yaml` in `postBuild.substitute`
2. Copy the existing application implementation in `apps/base/APP` and `apps/base/production` (OR `apps/base/staging`)
3. Change name of variables inside `release.yaml` by highlighting APP keyword and using shortcut Ctrl + Shift + L 

## STEPS TO DEPLOY NEW INFRASTRUCTURE APPLICATION/CONTROLLER
- When deploying infrastructure app there's no distinction between production and staging.  

1. You define your HelmRelease inside `infrastructure/controllers/release.yaml`  
2.  You need to add a resource to your release.yaml inside `infrastructure/controllers/kustomization.yaml`  
3. Additional Resources need to be inside `infrastructure/configs/` and also need to be added to `infrastructure/configs/kustomization.yaml`

## HOW TO DECRYPT, ENCRYPT SECRETS WITH SOPS AND AGE
1. Proceed with the initial guide https://fluxcd.io/flux/guides/mozilla-sops/
> Following instructions will be for WSL
2. Put your generated keys with `age` inside default folder for sops keys, which is `$HOME/.config/sops/age/age.agekey`
3. Configure config file for `.sops.yaml` (Already in the repository). Put there your **public** `age` key
4. In your `$HOME/.bashrc` set `export SOPS_AGE_KEY_FILE="/home/cloufish/.config/sops/age/age.agekey"` 
5. Use `sops decrypt secrets.yaml --output=secrets.yaml` or `sops encrypt secrets.yaml --output=secrets.yaml`
6. However, **even better option** is to use VSCode Extension to automatically (This is tricky in Windows environment)