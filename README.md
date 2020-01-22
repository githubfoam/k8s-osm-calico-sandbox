# kubernetes sandbox
cross platform(freebsd,lin,win,mac..etc)


kubernetes
open source MANO
NFVI / VIM, VNF OPNFV
NFVi
microservice-based cloud-native Container Network Functions - CNFs

~~~~
>vagrant up
>vagrant ssh remotecontrol01
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/1_initial.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/2_kube-dependencies.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/3_masters.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/4_workers.yml

>vagrant ssh k8s-master01
$ kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   20m   v1.16.0
worker01       Ready    <none>   12m   v1.16.0
worker02       Ready    <none>   12m   v1.16.0
$ kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-55754f75c-kckwb   1/1     Running   0          19m
kube-system   calico-node-6qhgc                         1/1     Running   7          19m
kube-system   calico-node-8648z                         1/1     Running   0          11m
kube-system   calico-node-m4thf                         1/1     Running   0          11m
kube-system   coredns-5644d7b6d9-2844c                  1/1     Running   0          19m
kube-system   coredns-5644d7b6d9-2dwp2                  1/1     Running   0          19m
kube-system   etcd-k8s-master01                         1/1     Running   0          18m
kube-system   kube-apiserver-k8s-master01               1/1     Running   0          19m
kube-system   kube-controller-manager-k8s-master01      1/1     Running   0          18m
kube-system   kube-proxy-2cwcx                          1/1     Running   0          11m
kube-system   kube-proxy-7xbfz                          1/1     Running   0          11m
kube-system   kube-proxy-dfgxk                          1/1     Running   0          19m
kube-system   kube-scheduler-k8s-master01               1/1     Running   0          18m
~~~~
upgrade
~~~~
vagrant ssh remotecontrol01
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/initial.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/kube-dependencies.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/masters.yml
sudo ansible-playbook -i /vagrant/kube-cluster/hosts /vagrant/kube-cluster/workers.yml

vagrant ssh k8s-master01
$ kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   20m   v1.16.0
worker01       Ready    <none>   12m   v1.16.0
worker02       Ready    <none>   12m   v1.16.0
$ kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-55754f75c-kckwb   1/1     Running   0          19m
kube-system   calico-node-6qhgc                         1/1     Running   7          19m
kube-system   calico-node-8648z                         1/1     Running   0          11m
kube-system   calico-node-m4thf                         1/1     Running   0          11m
kube-system   coredns-5644d7b6d9-2844c                  1/1     Running   0          19m
kube-system   coredns-5644d7b6d9-2dwp2                  1/1     Running   0          19m
kube-system   etcd-k8s-master01                         1/1     Running   0          18m
kube-system   kube-apiserver-k8s-master01               1/1     Running   0          19m
kube-system   kube-controller-manager-k8s-master01      1/1     Running   0          18m
kube-system   kube-proxy-2cwcx                          1/1     Running   0          11m
kube-system   kube-proxy-7xbfz                          1/1     Running   0          11m
kube-system   kube-proxy-dfgxk                          1/1     Running   0          19m
kube-system   kube-scheduler-k8s-master01               1/1     Running   0          18m

$ apt-cache madison docker-ce
 docker-ce | 5:19.03.4~3-0~ubuntu-xenial
$ apt-cache madison kubelet | more
 kubelet |  1.16.2-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages


kube-dependencies.yml
# kubernetes_version : "=1.15.2-00"
kubernetes_version : "=1.16.0-00"
validated_dockerv: "=5:18.09.8~3-0~ubuntu-xenial"


Installing a pod network add-on
kubectl apply -f https://docs.projectcalico.org/v3.8/manifests/calico.yaml
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/

$ kubectl get pods -n kube-system
$ kubectl -n kube-system logs coredns-5644d7b6d9-cw9bg
~~~~

~~~~
vagrant@k8s-master:~$ apt-cache madison docker-ce
 docker-ce | 5:19.03.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:19.03.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.8~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.7~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.6~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.5~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.4~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.3~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.2~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
 docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages

 vagrant@k8s-master:~$ apt-cache madison kubelet
    kubelet |  1.15.2-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
    kubelet |  1.15.1-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
    kubelet |  1.15.0-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
    kubelet |  1.14.5-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
    kubelet |  1.14.4-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages
    kubelet |  1.14.3-00 | https://apt.kubernetes.io kubernetes-xenial/main amd64 Packages

~~~~
~~~~  
v1.15 Release Notes
The list of validated docker versions remains unchanged.
The current list is 1.13.1, 17.03, 17.06, 17.09, 18.06, 18.09. (#72823, #72831)
https://kubernetes.io/docs/setup/release/notes/

Container runtimes
On each of your machines, install Docker. Version 18.06.2 is recommended, but 1.11, 1.12, 1.13, 17.03 and 18.09 are known to work as well. Keep track of the latest verified Docker version in the Kubernetes release notes.
https://kubernetes.io/docs/setup/production-environment/container-runtimes/

[WARNING IsDockerSystemdCheck]: detected "cgroupfs" as the Docker cgroup driver. The recommended driver is "systemd". Please follow the guide at https://kubernetes.io/docs/setup/cri/

~~~~
~~~~
vagrant@k8s-master01:~$ kubectl get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   14m   v1.15.2
worker01       Ready    <none>   11m   v1.15.2
worker02       Ready    <none>   11m   v1.15.2
vagrant@k8s-master01:~$ kubectl get pods --all-namespaces
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-5df986d44c-c6gwx   1/1     Running   0          5m38s
kube-system   calico-node-cfjfk                          1/1     Running   1          5m37s
kube-system   calico-node-kdqlh                          1/1     Running   0          3m54s
kube-system   calico-node-x84gg                          1/1     Running   0          4m7s
kube-system   coredns-5c98db65d4-2gqpk                   1/1     Running   0          5m37s
kube-system   coredns-5c98db65d4-j6kpd                   1/1     Running   0          5m37s
kube-system   etcd-k8s-master01                          1/1     Running   0          4m55s
kube-system   kube-apiserver-k8s-master01                1/1     Running   0          5m3s
kube-system   kube-controller-manager-k8s-master01       1/1     Running   0          5m
kube-system   kube-proxy-mxqvt                           1/1     Running   0          5m37s
kube-system   kube-proxy-rl45d                           1/1     Running   0          4m7s
kube-system   kube-proxy-s7ks9                           1/1     Running   0          3m54s
kube-system   kube-scheduler-k8s-master01                1/1     Running   0          5m9s
~~~~



Controlling your cluster from machines other than the control-plane node
~~~~
vagrant@k8s-master01:~$ hostnamectl | grep "Operating System"
  Operating System: Ubuntu 19.04
vagrant@worker01:~$ hostnamectl | grep "Operating System"
    Operating System: Ubuntu 16.04.5 LTS
vagrant@worker02:~$ hostnamectl | grep "Operating System"
      Operating System: Ubuntu 18.10


[vagrant@remotecontrol01 ~]$ cat /etc/redhat-release
CentOS Linux release 7.6.1810 (Core)


@k8s-master01:/etc/kubernetes/admin.conf .
copy the administrator kubeconfig file from your control-plane node to your workstation
scp vagrant@k8s-master01:/~admin.conf .

Install kubectl
[vagrant@remotecontrol01 ~]$ cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
[vagrant@remotecontrol01 ~]$ sudo yum install -y kubectl
[vagrant@remotecontrol01 ~]$ kubectl --kubeconfig ./admin.conf get nodes
NAME           STATUS   ROLES    AGE   VERSION
k8s-master01   Ready    master   38m   v1.15.2
worker01       Ready    <none>   31m   v1.15.2
worker02       Ready    <none>   30m   v1.15.2

~~~~

~~~~
Open Platform for NFV (OPNFV) 
https://wiki.opnfv.org/display/COM

Open Source MANO kubernetes deployment
https://github.com/egonzalez90/osm-k8s
~~~~
