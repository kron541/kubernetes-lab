# kubernetes-lab
Vagrantfile to create and provision three nodes with kubernetes.
## Requiriments
* Vagrant
* [Vagrant Libvirt Provider](https://github.com/vagrant-libvirt/vagrant-libvirt "Vagrant Libvirt Provider")
* Libvirt
* Ansible

## Node - IP address
| host  | ip address     |
|-------|----------------|
| node1 | 192.168.200.11 |
| node2 | 192.168.200.12 |
| node3 | 192.168.200.13 |
### single control-plane cluster
#### master node(e.g. node1)
    kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=192.168.200.11
    export KUBECONFIG=/etc/kubernetes/admin.conf
    kubectl apply -f https://docs.projectcalico.org/v3.11/manifests/calico.yaml
#### worker node(e.g. node2, node3)
    kubeadm join --token <token> <control-plane-host>:<control-plane-port> --discovery-token-ca-cert-hash sha256:<hash>
