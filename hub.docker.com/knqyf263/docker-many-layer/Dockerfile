FROM centos:7

RUN echo 'root:root' | chpasswd

RUN yum -y update
RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm
RUN yum -y install git vim python36u python36u-libs python36u-devel python36u-pip

RUN pip3.6 install --upgrade pip
RUN pip3.6 install django
RUN mkdir /app
WORKDIR /app
RUN echo foo > foo.txt

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.10.3/bin/linux/amd64/kubectl 
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/

RUN useradd -m git

CMD ["/bin/sh"]

