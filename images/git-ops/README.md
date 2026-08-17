# git-ops

GitOps tooling image based on [Wolfi OS](https://wolfi.dev/), providing
Flux, ArgoCD, Helm, kubectl, and Kustomize for GitOps workflows and
Kubernetes cluster management.

## Included Tools

- **Argo CD** (`argo-cd-3.4`) - GitOps continuous delivery tool for Kubernetes
- **Flux** (`flux-2.9`) - GitOps toolkit for Kubernetes
- **Helm** - Kubernetes package manager
- **kubectl** - Kubernetes command line tool
- **Kustomize** - Kubernetes configuration management
- **jq/yq** - JSON/YAML processors
- **git** - Version control system
- **OpenSSH Client** - Secure shell client for Git operations over SSH

## Versions

| 📌 Version | ⬇️ Pull URL                                          |
| ---------- | --------------------------------------------------- |
| latest     | ghcr.io/nlamirault/atoma/git-ops:latest        |
| latest-dev | ghcr.io/nlamirault/atoma/git-ops:latest-dev    |

## ✅ Verify the Build Provenance

GitHub CLI ([gh](https://cli.github.com/)) can be used to retrieve the build
provenance, which details the exact commit, workflow, and runner that produced
the image:

- **Production image**

```shell
gh attestation verify \
  --owner nlamirault \
  oci://ghcr.io/nlamirault/atoma/git-ops:latest
```

- **Dev image**

```shell
gh attestation verify \
  --owner nlamirault \
  oci://ghcr.io/nlamirault/atoma/git-ops:latest-dev
```

### Using Cosign

- **Production image**

```shell
cosign verify-attestation \
  --type slsaprovenance \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity-regexp '^https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_container_slsa3.yml@refs/tags/v[0-9]+.[0-9]+.[0-9]+$' \
  ghcr.io/nlamirault/atoma/git-ops:latest@sha256:xxxxxx
```

- **Dev image**

```shell
cosign verify-attestation \
  --type slsaprovenance \
  --certificate-oidc-issuer https://token.actions.githubusercontent.com \
  --certificate-identity-regexp '^https://github.com/slsa-framework/slsa-github-generator/.github/workflows/generator_container_slsa3.yml@refs/tags/v[0-9]+.[0-9]+.[0-9]+$' \
  ghcr.io/nlamirault/atoma/git-ops:latest-dev@sha256:xxxxxx
```

## ✅ Verify the Image Signature

All official images are **cryptographically signed** using
[Sigstore Cosign](https://www.sigstore.dev/).

- **Production image**

```shell
cosign verify \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/git-ops.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/git-ops:latest | jq
```

- **Dev image**

```shell
cosign verify \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/release.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/git-ops:latest-dev | jq
```

## ✅ Verify the Image Attestations

- **Production image**

```shell
cosign verify-attestation \
  --type=https://spdx.dev/Document \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com \
  --certificate-identity=https://github.com/nlamirault/atoma/.github/workflows/release.yaml@refs/heads/main \
  ghcr.io/nlamirault/atoma/git-ops:latest
```

## 📦 Download the Image SBOM Attestations

```shell
cosign download attestation \
  --platform=linux/amd64 \
  --predicate-type=https://spdx.dev/Document \
  ghcr.io/nlamirault/atoma/git-ops:latest | jq -r .payload | base64 -d | jq .predicate
```
