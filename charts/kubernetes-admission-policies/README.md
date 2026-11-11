# kubernetes-admission-policies

![Version: 0.2.0](https://img.shields.io/badge/Version-0.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

Kubernetes-native admission policies using ValidatingAdmissionPolicy and MutatingAdmissionPolicy with their policy bindings

**Homepage:** <https://github.com/kattler/charts>

## Installation

The chart is distributed only as an OCI artifact on ghcr.io, so `helm search repo` does not work. List versions with [crane](https://github.com/google/go-containerregistry/blob/main/cmd/crane/README.md):

```console
crane ls ghcr.io/kattler/charts/kubernetes-admission-policies
```

Install:

```console
helm install kubernetes-admission-policies oci://ghcr.io/kattler/charts/kubernetes-admission-policies \
  --version 0.2.0 \
  -f values.yaml
```

Inspect the chart before installing:

```console
helm show values oci://ghcr.io/kattler/charts/kubernetes-admission-policies --version 0.2.0
```

Upgrade and uninstall:

```console
helm upgrade kubernetes-admission-policies oci://ghcr.io/kattler/charts/kubernetes-admission-policies --version 0.2.0 -f values.yaml
helm uninstall kubernetes-admission-policies
```

## Requirements

Kubernetes: `>=1.30.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| nameOverride | string | `""` | Override chart name |
| fullnameOverride | string | `""` | Override full resource names |
| commonLabels | object | `{}` | Labels applied to all resources |
| commonAnnotations | object | `{}` | Annotations applied to all resources |
| apiVersions.validatingAdmissionPolicy | string | `"admissionregistration.k8s.io/v1"` | apiVersion used for ValidatingAdmissionPolicy and ValidatingAdmissionPolicyBinding resources |
| apiVersions.mutatingAdmissionPolicy | string | `"admissionregistration.k8s.io/v1"` | apiVersion used for MutatingAdmissionPolicy and MutatingAdmissionPolicyBinding resources. Use `admissionregistration.k8s.io/v1beta1` on Kubernetes 1.34, `admissionregistration.k8s.io/v1` on 1.35+ |
| validatingAdmissionPolicies | object | `{}` | ValidatingAdmissionPolicy resources keyed by policy name. Each policy and each binding has its own `enabled` toggle. Object and string fields are rendered through `tpl`, so Helm template expressions are supported. [Kubernetes Docs](https://kubernetes.io/docs/reference/access-authn-authz/validating-admission-policy/) |
| mutatingAdmissionPolicies | object | `{}` | MutatingAdmissionPolicy resources keyed by policy name. Each policy and each binding has its own `enabled` toggle. Object and string fields are rendered through `tpl`. Requires Kubernetes 1.34+ (beta). [Kubernetes Docs](https://kubernetes.io/docs/reference/access-authn-authz/mutating-admission-policy/) |
| extraObjects | list | `[]` | Extra Kubernetes objects to deploy alongside the chart. Entries can be plain objects or strings, both rendered through `tpl` so Helm template expressions are supported |
