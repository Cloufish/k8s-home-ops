# flux2-kustomize-helm-example

[![test](https://github.com/fluxcd/flux2-kustomize-helm-example/workflows/test/badge.svg)](https://github.com/fluxcd/flux2-kustomize-helm-example/actions)
[![e2e](https://github.com/fluxcd/flux2-kustomize-helm-example/workflows/e2e/badge.svg)](https://github.com/fluxcd/flux2-kustomize-helm-example/actions)
[![license](https://img.shields.io/github/license/fluxcd/flux2-kustomize-helm-example.svg)](https://github.com/fluxcd/flux2-kustomize-helm-example/blob/main/LICENSE)

For this example we assume a scenario with two clusters: staging and production.
The end goal is to leverage Flux and Kustomize to manage both clusters while minimizing duplicated declarations.

We will configure Flux to install, test and upgrade a demo app using
`HelmRepository` and `HelmRelease` custom resources.
Flux will monitor the Helm repository, and it will automatically
upgrade the Helm releases to their latest chart version based on semver ranges.
## STEPS TO DEPLOY NEW APPLICATION
1. In define ${APP_app_name} variable in `clusters/production/apps.yaml` in `postBuild.substitute`
2. Copy the existing application implementation in `apps/base/APP` and `apps/base/production` (OR `apps/base/staging`)
3. Change name of variables inside `release.yaml` by highlighting APP keyword and using shortcut Ctrl + Shift + L 

## STEPS TO DEPLOY NEW INFRASTRUCTURE APPLICATION/CONTROLLER
- When deploying infrastructure app there's no distinction between production and staging.  

1. You define your HelmRelease inside `infrastructure/controllers/release.yaml`  
2.  You need to add a resource to your release.yml inside `infrastructure/controllers/kustomization.yaml`  
3. Additional Resources need to be inside `infrastructure/configs/` and also need to be added to `infrastructure/configs/kustomization.yaml`
