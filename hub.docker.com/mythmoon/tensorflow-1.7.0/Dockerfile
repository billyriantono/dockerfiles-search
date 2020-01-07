####ansible2-->tensorflow==1.7.0
FROM ubuntu:17.10
RUN mkdir /kubeflow
WORKDIR /kubeflow
RUN apt update -y && \
    apt install -y \
    libssl-dev python-dev sshpass apt-transport-https \
    ca-certificates curl gnupg2 software-properties-common python-pip wget  vim
RUN /usr/bin/python -m pip install pip -U 
RUN pip install --no-cache-dir pbr>=1.6 ansible>=2.4.0 netaddr jinja2>=2.9.6 
RUN pip install --no-cache-dir yamllint apache-libcloud==2.2.1 boto==2.9.0 tox dopy PyCrypto
RUN pip install --no-cache-dir absl-py==0.1.13  astor==0.6.2 backports.weakref==1.0.post1
RUN pip install --no-cache-dir bleach==1.5.0 enum34==1.1.6 funcsigs==1.0.2 futures==3.2.0
RUN pip install --no-cache-dir grpcio==1.10.1 html5lib==0.9999999 Markdown==2.6.11 mock==2.0.0
RUN pip install --no-cache-dir numpy==1.14.2 pbr==4.0.1 protobuf==3.5.2.post1 six==1.11.0 termcolor==1.1.0 Werkzeug==0.14.1
RUN pip install --no-cache-dir tensorflow==1.7.0 tensorflow-serving-api==1.7.0 tensorboard==1.7.0






