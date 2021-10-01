# Gitops InstallPlan Approver

Allow for the installation of Operators and the auto approval of the install plan during an argo deploy when usinging manual approval method

## Usage

Add the following kustomization.yaml into a folder and refer to it from the main Operator Kustomise location

```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

namePrefix: <name-of-subscription>-
namespace: <operator-subcription-namespace>

bases:
- https://github.com/Siythrun/gitops-installplan-approver

```
### Sync Waves

This repo manke use of Sync Waves to have Objects apply in the correct order by deafult it is set to 1 therefor for any manifest that you would like to have run after the Operator is installed will need the following Annotaion.


```
metadata:
  annotations:
    argocd.argoproj.io/sync-wave: "2"
    argocd.argoproj.io/sync-options: SkipDryRunOnMissingResource=true
```

More info on sync waves can be found https://argoproj.github.io/argo-cd/user-guide/sync-waves/
