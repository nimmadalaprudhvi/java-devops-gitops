# Setup

## 1. GitOps repository

Create/push these files to:

https://github.com/nimmadalaprudhvi/java-devops-gitops

## 2. GitHub token

The application repository needs a secret named:

GITOPS_TOKEN

The token must be allowed to push to the `nimmadalaprudhvi/java-devops-gitops` repository.

Keep `AWS_ROLE_TO_ASSUME` and `SONAR_TOKEN` as existing secrets.

## 3. Argo CD

Apply `argocd/application.yaml` after Argo CD is installed and the EKS cluster is reachable:

kubectl apply -f argocd/application.yaml

Argo CD will track:

apps/java-devops-sample

on the `main` branch.

## 4. Image update

The CI workflow pushes:

<account>.dkr.ecr.ap-south-1.amazonaws.com/java-devops-sample:<commit-sha>

Then it changes only the `image:` line in:

apps/java-devops-sample/deployment.yaml

and pushes that change to the GitOps repository.

Argo CD sees the Git commit and deploys the new image to EKS.
