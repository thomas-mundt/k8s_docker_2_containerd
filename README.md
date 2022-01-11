# Migrate Docker to Containerd

```
ctr namespace list
ctr --namespace moby container list

k cordon worker1
k drain worker1 --ignore-daemonsets --force --delete-local-data

systemctl stop kubelet
systemctl stop docker

apt purge docker-ce docker-ce-cli

vi /etc/containerd/config.toml
#comment line

systemctl restart containerd
vi /var/lib/kubelet/kubeadm-flags.env
# Add
--cgroup-driver=systemd 
--resolv-conf=/run/systemd/sesolve/resolv.conf 
--container-runtime=remote
--container-runtime-endpoint=unix:///run/containerd/containerd.sock

systemctl start kubelet
reboot

k get no -o wide


```

