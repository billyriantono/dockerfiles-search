FROM centos:7

RUN yum update -y
RUN yum install wget -y 
RUN yum install vim -y 

#install kops tool 
RUN wget -O kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
RUN chmod +x ./kops
RUN mv ./kops /usr/local/bin/

#install kubectl tool 

RUN wget -O kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

#install AWS CLI 
RUN  yum -y update
RUN  curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN  python get-pip.py
RUN  pip install awscli

#install 
RUN yum -y install openssh-server openssh-clients

#install Helm 
RUN yum install openssl -y
RUN yum install which -y
RUN curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
RUN chmod 700 get_helm.sh
RUN ./get_helm.sh

#
