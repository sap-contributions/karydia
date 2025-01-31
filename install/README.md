# Installation
Karydia can be installed as a webhook into any Kubernetes cluster.

The installation processes uses [Helm](https://github.com/helm/helm) to get Karydia up and running and is split up into two parts.

You can also do an [installation by hand](../docs/manualInstallation.md) without Helm.

## Delpoy Karydia
To deploy Karydia first create the specified namespace and install Karydia:
```
kubectl create namespace karydia
helm install karydia ./install/charts --namespace karydia
```

## Make sure that Karydia is runnning
Afterwards, you can check if Karydia is running by taking a look at the logs:
```
kubectl logs -n karydia $(kubectl get pods -n karydia -l app=karydia -o jsonpath='{.items[0].metadata.name}') -f -c karydia
```

Karydia is up and running, if the following information is logged:
```
{"component":"server","level":"info","msg":"[INFO] Listening on 0.0.0.0:33333","time":"2019-08-22T10:47:50Z"}
[...]
```

## Development
If you want to install the development image, simply run:
```
kubectl create namespace karydia
helm install karydia ./install/charts --namespace karydia --set dev.active=true
```
Otherwise, you can set `dev.active` to `true` in the `values.yaml` file.
