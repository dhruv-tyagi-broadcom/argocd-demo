# GitOps for VKS clusters, VMs and apps with Argo CD on VCF 9.1

One Git repo drives everything: VKS clusters, VMs, and the apps running on them.

## How it's organised

| Folder | What it is |
|---|---|
| `infra/platform/` | Platform setup: lets Argo CD auto-attach any VKS cluster labelled `env: dev` or `env: prod` |
| `infra/<env>/` | One folder per environment: a VKS cluster and a VM |
| `apps/demo-app/<env>/` | What runs on each environment's VKS cluster |
| `argocd/` | Tells Argo CD about the two folders above |

**The rule:** a cluster labelled `env: prod` is attached to Argo CD automatically and gets `apps/demo-app/prod`.

## Add a new environment

Open a pull request that adds `infra/prod/` (a VKS cluster labelled `env: prod` and a VM). After it's merged:

1. Argo CD creates the VKS cluster and the VM.
2. The cluster attaches itself to Argo CD with `env=prod`.
3. Argo CD deploys `apps/demo-app/prod` to it.

## Promote a change

Change `apps/demo-app/dev/app.yaml` and check it in dev, then open a pull request making the same change in `apps/demo-app/prod/app.yaml`.
