# docs-glueops-platform

This repo outlines how to install the GlueOps Platform using a helm chart. This is part of the opionated GlueOps Platform. If you came here directly then you should probably visit https://github.com/glueops/admiral as that is the starting point.

# Prerequisites

- Connection to the Kubernetes server. The authentication methods will vary by Cloud Provider and are documented within their respective wikis.
- You must have already installed ArgoCD

## Deploying the GlueOps Platform Helm Chart

- Prepare a `platform.yaml` to use for the GlueOps Platform installation. 
  - Please reference the `values.yaml` from the [platform chart](https://github.com/GlueOps/platform-helm-chart-platform)
  - We recommend copying the `values.yaml` and saving it as your `platform.yaml` and then updating values as needed. There are inline comments next to each value.
  - Quick Notes:
    - Replace `<tenant-name-goes-here>` with your tenant/company key. Example: `antoniostacos`
    - Replace `<cluster_env> with your` cluster_environment name. Example: `nonprod`
    - As mentioned in the ArgoCD docs, the ArgoCD's `clientSecret` needs to match the ArgoCD `client_secret` you define within this `platform.yaml`.

```bash
helm repo add glueops-platform https://helm.gpkg.io/platform
helm install glueops-platform glueops-platform/glueops-platform --version 0.11.0 -f platform.yaml --namespace=glueops-core
```

- Check on ArgoCD application status with

```bash
kubectl get applications -n glueops-core
```

With the exception of vault all the ArgoCD applications should become healthy within 20mins.
