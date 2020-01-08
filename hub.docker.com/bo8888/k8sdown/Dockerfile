FROM centos
RUN yum install yum-utils -y
RUN echo "[kubernetes]" >/etc/yum.repos.d/k9s.repo
RUN echo "name=Kubernetes" >>/etc/yum.repos.d/k9s.repo
RUN echo "baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64" >>/etc/yum.repos.d/k9s.repo
RUN echo "enabled=1" >>/etc/yum.repos.d/k9s.repo
RUN echo "gpgcheck=0" >>/etc/yum.repos.d/k9s.repo
RUN yumdownloader kubernetes-cni kubelet kubectl kubeadm
