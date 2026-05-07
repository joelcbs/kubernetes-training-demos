# kubernetes-training-demos
kubernetes demo training
this file is frrom joel
INSTALLATION OF KUBERNeTES  CLUSTER 

Step1: Install the CRE  (i,e cri-o)

open the website in the web-broswer    https://cri-o.io/



Define the Kubernetes version and used CRI-O stream
KUBERNETES_VERSION=v1.32CRIO_VERSION=v1.32   (  on master  and node1 and node2)


Distributions using rpm packagesAdd the Kubernetes repository (  on master  and node1 and node2)
cat <<EOF | tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/rpm/repodata/repomd.xml.keyEOF


Add the CRI-O repository    (  on master  and node1 and node2)
cat <<EOF | tee /etc/yum.repos.d/cri-o.repo
[cri-o]
name=CRI-O
baseurl=https://download.opensuse.org/repositories/isv:/cri-o:/stable:/$CRIO_VERSION/rpm/
enabled=1
gpgcheck=1
gpgkey=https://download.opensuse.org/repositories/isv:/cri-o:/stable:/$CRIO_VERSION/rpm/repodata/repomd.xml.keyEOF

 

Install package dependencies from the official repositories  (  on master  and node1 and node2)
dnf install -y container-selinux


Install the packages (  on master  and node1 and node2)
dnf install -y cri-o kubelet kubeadm kubectl

Start CRI-O (  on master  and node1 and node2)
systemctl start crio.service


Bootstrap a cluster  (  on master  and node1 and node2)
swapoff -a
modprobe br_netfilter
sysctl -w net.ipv4.ip_forward=1

