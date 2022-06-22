# three-tier-chart-with-mongodb
This chart deploys a three tier application. [reactapp](https://github.com/yogeshlonkar/reactapp) is used as front-end, [nodeapp](https://github.com/yogeshlonkar/nodeapp) as back-end along with mongodb `StatefulSet`. This chart also exposes Ingress service for `nodeapp`. The chart manages depdendency between different pods using [pod-dependency-init-container](https://github.com/yogeshlonkar/pod-dependency-init-container).

Prerequisites

- Kubernetes 1.8+
- helm 2.10+

## Installing the Chart
To install the chart with the release name my-release:
```shell
$ helm install . -n my-release
```

## For upgrade
After modifying app images/tags in yaml below can be used to upgrade app
```shell
$ helm upgrade my-release .
```

## Uninstalling the Chart
To uninstall/delete the my-release deployment:
```shell
$ helm delete my-release
```

## Persistence
Chart whill create `StorageClass`, `PersistanceVolume` and `PersistanceVolumeClaim`.
- Mongodb urls will be `templatized` in [`_helper.tpl`](templates/_helpers.tpl) which is injected as env in `nodeapp` containers
- Note: uninstalling chart will not remove `PersistanceVolume` and `PersistanceVolumeClaim`, They need to be manually removed.

## RBAC
[`service-account.yaml`](templates/rbac/service-account.yaml) creates a service account which is used by `pod-dependency-init-container` to resolve pod dependecies.
