FROM centos:7
RUN yum update -y 
RUN yum install -y epel-release
RUN yum update -y && \
    yum install -y git curl wget which git python-pip unzip && \
    pip install --upgrade pip && \
    pip install awscli --upgrade && \
    curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64 && \
    chmod +x kops-linux-amd64 && \
    mv kops-linux-amd64 /usr/local/bin/kops && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/kubernetes-client-linux-amd64.tar.gz && \
    tar -xzvf kubernetes-client-linux-amd64.tar.gz && \
    cp kubernetes/client/bin/kubefed /usr/local/bin && \
    chmod +x /usr/local/bin/kubefed && \
    cp kubernetes/client/bin/kubectl /usr/local/bin && \
    chmod +x /usr/local/bin/kubectl && \
    curl  -LO https://releases.hashicorp.com/terraform/0.11.0/terraform_0.11.0_linux_amd64.zip && \
    unzip terraform_0.11.0_linux_amd64.zip
