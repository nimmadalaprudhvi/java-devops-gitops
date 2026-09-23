# java-devops-gitops

GitOps repository for the `java-devops-sample` application.

Flow:

GitHub Actions CI
  -> build/test
  -> SonarCloud
  -> Docker build
  -> Trivy
  -> push immutable image to ECR
  -> update `apps/java-devops-sample/deployment.yaml`
  -> commit/push to this repository
  -> Argo CD detects the Git change
  -> Argo CD syncs Kubernetes manifests
  -> EKS
  -> AWS Load Balancer Controller
  -> AWS ALB

Only Kubernetes application manifests belong in this repository.
Terraform infrastructure stays in the Terraform repository.

Do not manually edit the image tag after CI/CD is configured.
