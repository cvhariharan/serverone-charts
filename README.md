## SERVERONE
Helm chart to deploy serverone services on K3S.

### Deploy
```
helm upgrade --install serverone serverone/ --values values-prod.yaml
```
### Services
Included in this chart
- [Pi-Hole](https://github.com/pi-hole/pi-hole)
- [Miniflux](https://github.com/miniflux/v2) ( with Postgres )
- [Excalidraw](https://github.com/excalidraw/excalidraw)
- [QBittorrent](https://github.com/qbittorrent/qBittorrent)
- [Jellyfin](https://github.com/jellyfin/jellyfin)
- [Prometheus](https://github.com/prometheus/prometheus)
- [Grafana](https://github.com/grafana/grafana)
- [Flame](https://github.com/pawelmalak/flame)

Other services on the cluster
- [Longhorn](https://github.com/longhorn/longhorn)
- [Samba CSI](https://github.com/kubernetes-csi/csi-driver-smb)

### Nvidia Setup
Nvidia GPU is used for hardware acceleration in Jellyfin.
K3S has nvidia container runtime support. https://docs.k3s.io/advanced#nvidia-container-runtime-support
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
