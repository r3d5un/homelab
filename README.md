# Homelab

This repo contains Kubernetes manifest files which can be used to setup a homelab or complete local development setup. As is, the manifest files are aimed towards a single node MicroK8s, but should serve well as a starting point for any other Kubernetes distribution.

## Setup

Some apps in this repository require extra setup, for example, persistent storage for databases.

### Persistent Storage

Kubernetes does not come with any default storage solutions, which makes persistent storage rely on other solutions. MicroK8s solves this problem in several ways, one of which is using [hostpath-storage](https://microk8s.io/docs/addon-hostpath-storage).

Activating the hostpath storage is a simple as enabling the addon.

```bash
microk8s enable hostpath-storage
```

The storage can then be made available to apps in the form of a storage class, of which an example can be found in [here](./kubernetes/hostpath-access-stroage-class.yaml).

You can apply the manifest file directly with the following command, though you made have to adjust the path.

```bash
kubectl apply -f kubernetes/hostpath-access-stroage-class.yaml
```

Applications included in this repository will also contain manifest for persistent volumes and persistent volume claims built on the hostpath access storage class.
