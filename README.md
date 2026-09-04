# gha-shared

Reusable GitHub Actions workflows for Jason’s private lab repos.

Public repos (like `opentofu`) cannot call workflows from a **private** repository. Keep this private and call it from private apps. To share with public repos later, make this repository public.

Access: this repo’s Actions settings must allow access from other repositories owned by `jason4151`.

## Workflows

### `node-docker-ci.yml`

Lint, Vite/npm build, and a local Docker build (no AWS).

```yaml
jobs:
  ci:
    uses: jason4151/gha-shared/.github/workflows/node-docker-ci.yml@main
    with:
      node_version: "22"
```

### `ecr-eks-deploy.yml`

OIDC to `GitHubActionsRole`, push to ECR, Helm deploy onto `lab-eks-cluster`.

Caller needs repo secret `AWS_ACCOUNT_ID`. The EKS cluster and ECR repository must already exist (OpenTofu lab).

```yaml
jobs:
  deploy:
    uses: jason4151/gha-shared/.github/workflows/ecr-eks-deploy.yml@main
    secrets: inherit
    with:
      ecr_repository: lab/subnet-calculator
      release_name: subnet-calculator
      helm_chart: helm
      namespace: lab
```
