FROM amazonlinux:2.0.20190228

ENV GOSRC  go1.13.3.linux-amd64
ENV GOPATH /go
ENV PATH   $PATH:/usr/local/go/bin:/go:/go/bin

RUN echo "Install OS dependencies" && \
      yum -y install \
        gcc \
        git \
        ImageMagick \
        ImageMagick-devel \
        make \
        python2-devel \
        python2-pip \
        rsync \
        tar \
        unzip \
        wget \
        zip && \
    echo "Install Docker cli" && \
      yum -y install \
        yum-utils \
        device-mapper-persistent-data \
        lvm2 && \
      yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo && \
      yum -y install \
        docker-ce-cli && \
    echo "Install Go" && \
      wget -q https://dl.google.com/go/$GOSRC.tar.gz && \
      tar -xvf $GOSRC.tar.gz && \
      mv go /usr/local && \
      rm $GOSRC.tar.gz && \
      mkdir /go && \
    echo "Install AWS SAM CLI" && \
      pip install --upgrade --force-reinstall pip==19.3.1 && \
      pip install aws-sam-cli==0.23.0 && \
    echo "Install ngrok.." && \
      wget -q https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip && \
      unzip ngrok-stable-linux-amd64.zip -d /usr/bin && \
      rm -f ngrok-stable-linux-amd64.zip && \
    echo "Cleanup.." && \
      yum -y remove \
        python2-devel && \
      rm -Rf /var/cache/yum/* && \
      yum clean all
