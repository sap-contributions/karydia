# Karydia - A Kubernetes Security Walnut

![Karydia Logo](logo/Karydia@0.5x.png)

**Status: Beta** | **Kubernetes Version >=1.15.x**

Karydia is a security add-on for Kubernetes, which helps you follow good security practices by inverting insecure default settings in Kubernetes. Kubernetes default settings are not optimized for security, but rather on running out-of-the-box without complicated configuration upfront. It's easy to get a pod up and running; in the simplest case it's just one command. Unfortunately, the simple setup does not have a highly secure application in mind. Default settings are not enough!

Karydia inverts the following insecure default settings:
* Unmount service account token
* Restrict system calls by adding a seccomp profile
* Run with minimal privileges by adding a non-root user
* Disallow privilege escalation
* Restrict network communication by automatically adding one or multiple network policies to each namespace

A description of each feature can be found [here](docs/features.md) and an overview of the application of these features is described in the [demo section](docs/demos/overview.md).

If you have any problems while using Karydia, have a look at our [troubleshooting guide](docs/troubleshooting.md). If this does not solve your problem, please open a [GitHub Issue](https://github.com/karydia/karydia/issues/new?assignees=&labels=bug&template=bug_report.md&title=).

## Installing Karydia
To install Karydia using Helm run the following commands:
```
kubectl create namespace karydia
helm install karydia ./install/charts --namespace karydia
```

A detailed description of the installation process can be found in the [corresponding readme](install/README.md).

## Testing

### Integration Tests

##### Install Karydia Dev
```
kubectl create namespace karydia
helm install karydia ./install/charts --namespace karydia --set dev.active=true
```

##### Build, Swap and Test

```
make build deploy-dev
make e2e-test
```

### Unit Tests

```
make test
```

### Debug Karydia

To debug (for example Visual Studio Code), change the following line in the debug configuration:

```
"args": ["--kubeconfig","<PATH>/.kube/config"]
```
