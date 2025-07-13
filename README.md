<div align="center">

## My Home Operations repository

_... managed by Flux, and GitHub Actions_ :robot:


</div>
<br>
This repository is meant for me to configure and manage my cluster.
And to learn more K8s concepts and GitOps, DevOps 
I'll try to create my own (Helm Charts)[https://github.com/Cloufish/helm-charts]

## STEPS TO DEPLOY NEW APPLICATION
1. In define ${APP_app_name} variable in `clusters/production/apps.yaml` in `postBuild.substitute`
2. Copy the existing application implementation in `apps/base/APP` and `apps/base/production` (OR `apps/base/staging`)
3. Change name of variables inside `release.yaml` by highlighting APP keyword and using shortcut Ctrl + Shift + L 

## STEPS TO DEPLOY NEW INFRASTRUCTURE APPLICATION/CONTROLLER
- When deploying infrastructure app there's no distinction between production and staging.  

1. You define your HelmRelease inside `infrastructure/controllers/release.yaml`  
2.  You need to add a resource to your release.yml inside `infrastructure/controllers/kustomization.yaml`  
3. Additional Resources need to be inside `infrastructure/configs/` and also need to be added to `infrastructure/configs/kustomization.yaml`
