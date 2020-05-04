# cEOSR/Kubernetes for Cilium

# Versions Supported
## Kubernetes Version
Kubernetes 1.16

## Linux Distro/Kernel
CentOS Linux release: 7.7/7.6
Kernel : 3.10

## Docker version:
Docker 18.06 with systemd cgroup driver

## Cilium
Cilium 1.7 or later

# How To Deploy

- Deploy Cilium following the [Cilium guide](https://cilium.readthedocs.io/en/stable/gettingstarted/k8s-install-default/), but instead of deploying the YAML file directly, download it to your local machine to make changes
- Edit the YAML file entry to remove overlay:

```
  # Encapsulation mode for communication between nodes
  # Possible values:
  #   - disabled
  #   - vxlan (default)
  #   - geneve
  tunnel: disabled
```
- Deploy the Cilium YAML file.  (i.e. `kubectl apply -f quick-install.yaml`)

- Apply node annotations if desired (see root page of repo.  It is suggested to annotate with BGP settings)
- Download the `cloudeos-cilium.yaml` file located in this directory
- Make any needed changes to the example yaml file
- Deploy the cloudeos yaml file:

```
    kubectl apply -f cloudeos-cilium.yaml
``` 
# User configurable Parameters 
Refer to the CloudEOS parameters in the [project root directory](https://github.com/aristanetworks/cloudeos-k8s).
