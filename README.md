## SERVERONE
Helm chart to deploy serverone services on K3S.

### Deploy
```
kubectl create namespace monitoring # for deploying prometheus and grafana
helm upgrade serverone serverone/ --values values-prod.yaml
```
### Services
Included in this chart
- Pi-Hole
- Miniflux ( with Postgres )
- Excalidraw
- QBittorrent
- Jellyfin

Other services on the cluster
- Longhorn
- [Samba CSI](https://github.com/kubernetes-csi/csi-driver-smb)

### Nvidia Setup
K3S nvidia container runtime support. https://docs.k3s.io/advanced#nvidia-container-runtime-support
- Install [nvidia drivers](https://wiki.debian.org/NvidiaGraphicsDrivers)
- Install [nvidia-container-runtime](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
- Restart k3s

Label the node with nvidia support for use with Jellyfin.
```
kubectl label nodes <your-node-name> gpu=nvidia
```
Deploy nvidia k8s-device-plugin
https://github.com/NVIDIA/k8s-device-plugin#quick-start

```
helm install nvdp nvdp/nvidia-device-plugin --namespace nvidia-device-plugin --create-namespace --version 0.14.1 --set gfd.enabled=true
```
