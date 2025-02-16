# Helm Commands CheatSheet

A comprehensive cheatsheet covering essential Helm commands for managing Kubernetes applications efficiently.

## Table of Contents

- [Helm Basics](#helm-basics)
- [Chart Management](#chart-management)
- [Release Management](#release-management)
- [Values & Configuration](#values--configuration)
- [Debugging & Troubleshooting](#debugging--troubleshooting)
- [Helm Plugins & Hooks](#helm-plugins--hooks)
- [Security & Best Practices](#security--best-practices)

## Helm Basics

Initialize Helm (for Helm v2):
```bash
helm init
```

Verify Helm Installation:
```bash
helm version
```

List Available Repositories:
```bash
helm repo list
```

Add a Helm Repository:
```bash
helm repo add <repo-name> <repo-url>
```

Update Local Repository Cache:
```bash
helm repo update
```

Search for a Chart:
```bash
helm search repo <chart-name>
```

## Chart Management

Create a New Helm Chart:
```bash
helm create <chart-name>
```

Package a Helm Chart:
```bash
helm package <chart-name>
```

Lint a Chart for Errors:
```bash
helm lint <chart-name>
```

Push Chart to Repository:
```bash
helm push <chart.tgz> <repo-name>
```

## Release Management

Install a Helm Chart:
```bash
helm install <release-name> <chart-name> -n <namespace>
```

Upgrade a Release:
```bash
helm upgrade <release-name> <chart-name> -f values.yaml
```

Rollback to Previous Release:
```bash
helm rollback <release-name> <revision-number>
```

Uninstall a Release:
```bash
helm uninstall <release-name> -n <namespace>
```

List All Releases:
```bash
helm list --all-namespaces
```

Check Release History:
```bash
helm history <release-name>
```

## Values & Configuration

Show Default Values for a Chart:
```bash
helm show values <chart-name>
```

Override Values During Install:
```bash
helm install <release-name> <chart-name> --set key=value
```

Use a Custom `values.yaml` File:
```bash
helm install <release-name> <chart-name> -f values.yaml
```

Dry Run to Test Values:
```bash
helm install <release-name> <chart-name> -f values.yaml --dry-run --debug
```

Merge Multiple Values Files:
```bash
helm install <release-name> <chart-name> -f values1.yaml -f values2.yaml
```

## Debugging & Troubleshooting

Check Helm Release Status:
```bash
helm status <release-name>
```

View Logs of Failed Releases:
```bash
helm get manifest <release-name>
```

Check Rollback History:
```bash
helm history <release-name>
```

Debug a Chart Before Installation:
```bash
helm template <chart-name> -f values.yaml | kubectl apply --dry-run=client -f -
```

Run Helm Tests:
```bash
helm test <release-name>
```

## Helm Plugins & Hooks

List Installed Plugins:
```bash
helm plugin list
```

Install a Helm Plugin:
```bash
helm plugin install <plugin-url>
```

List All Hooks in a Chart:
```bash
helm show hooks <chart-name>
```

Add Pre-Install Hook in `templates/hooks.yaml`:
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pre-install-job
  annotations:
    "helm.sh/hook": pre-install
    "helm.sh/hook-delete-policy": before-hook-creation
```

## Security & Best Practices

Enable Helm Release Namespacing:
```bash
helm install <release-name> <chart-name> --namespace <namespace>
```

Verify Chart Integrity:
```bash
helm verify <chart.tgz>
```

Enforce TLS for Helm:
```bash
helm install <release-name> <chart-name> --tls
```

Restrict Tiller Permissions (for Helm v2):
```bash
kubectl create rolebinding tiller-binding --role=tiller-role --serviceaccount=kube-system:tiller
```

## Pro Tips

Render Templates Without Installing:
```bash
helm template <chart-name> -f values.yaml
```

Helm Debug Mode:
```bash
helm install <release-name> <chart-name> --debug --dry-run
```

Export Helm Values for a Running Release:
```bash
helm get values <release-name>
```

Generate Kubernetes YAML from Helm:
```bash
helm template <release-name> <chart-name> > output.yaml
```