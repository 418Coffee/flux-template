# (WIP) flux-template - An opinionated cluster agnostic Flux GitOps template repository

A lot of Flux template repositories expect you have already decided what type of Kubernetes distribution you want to use (i.e. the same one they are using). It works when your goals align with theirs but it can be a pain when they're even slightly off. This repository proposes the opposite approach, you know what core applications you want to run on your cluster, but you're not yet sure about the cluster infrastructure.

## Table of contents

- [Overview](#overview)
- [Quickstart](#quickstart)
- [Considerations](#considerations)
- [Contributing](#contributing)
- [License](#license)

## Overview

A fully set up repository structure is as follows:

### Top directories

- `.keys`: pgp public keys
- `apps`: user related deployments (e.g. webapps, game servers)
- `cluster`: Flux configuration
- `infrastructure`: common infrastructure components (e.g. monitoring, network)
- `templates`: yaml template files
- `tools`: workspace and template rendering

Flux is setup to only look at `apps`, `cluster` and `infrastructure`.

```
├── apps
│   └── kustomization.yaml
│  
├── cluster
│   ├── flux-system
│   ├── apps.yaml
│   └── infrastructure.yaml
|
└── infrastructure
    ├── configs
    ├── controllers
    ├── image-automations
    ├── notifications
    └── sources
```

#### Applications

The `apps` directory is very straightforward, you can structure it however you want as long as you mention the resource in the `kustomization.yaml` file.

#### Cluster

The `cluster` directory holds all the files necessary for Flux to work. The `flux-system` directory is generated after bootstrapping, the `apps.yaml` and `infrastructure.yaml` hold the Flux Kustomization definitions.

#### Infrastructure

The `infrastructure` is structured into 5 sub directories:

- `configs`: Kubernetes custom resources such as cert issuers and networks policies
- `controllers`: namespaces and Helm release definitions for Kubernetes controllers
- `image-automations`: [Image reflector and automation controllers](https://fluxcd.io/flux/components/image/)
- `notifications`: [Notification Controllers](https://fluxcd.io/flux/components/notification/)
- `sources`: [Source Controllers](https://fluxcd.io/flux/components/source/)

The `configs`, `image-automations`, `notifications` directories by default have no definitions. For brevity, they are omitted from the following view:

```
./infrastructure
├── controllers
│   ├── monitoring
|   ├── network
|   ├── upgrade
|   ├── reloader.yaml
|   └── kustomization.yaml
│  
└── sources
    ├── bucket
    ├── git
    ├── oci
    ├── helmrepos
    └── kustomization.yaml
```

The `controllers` and `sources` directories have the following sub directories respectively:

- `monitoring`: Monitoring controllers
- `network`: Network controllers
- `upgrade`: Upgrade controllers

- `bucket`: [Buckets](https://fluxcd.io/flux/components/source/buckets/)
- `git`: [GitRepositories](https://fluxcd.io/flux/components/source/gitrepositories/)
- `oci`: [OCIRepositories](https://fluxcd.io/flux/components/source/ocirepositories/)
- `helmrepos`: [HelmRepositories](https://fluxcd.io/flux/components/source/helmrepositories/)

## Quickstart

TODO

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
