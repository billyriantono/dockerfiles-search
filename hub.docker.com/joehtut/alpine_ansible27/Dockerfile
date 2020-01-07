FROM alpine
ENV ANSIBLE_VERSION 2.8
ENV container docker
ENV BUILD_PACKAGES \
  bash \
  curl \
  tar \
  python3 \
  ca-certificates \
  openssh-client \
  sshpass \
  git \
  py-boto \
  py-dateutil \
  py-httplib2 \
  py-jinja2 \
  py-pip \
  py-yaml \
  gnome-keyring \
  dbus

RUN echo "==> Adding build-dependencies..."  && \
    apk --update add --virtual build-dependencies \
      gcc \
      musl-dev \
      libffi-dev \
      libsodium-dev \
      openssl-dev \
      python3-dev && \
    \
    echo "==> Upgrading apk and system..."  && \
    apk update && apk upgrade && \
    \
    echo "==> Adding Python runtime..."  && \
    apk add --no-cache ${BUILD_PACKAGES} && \
    pip3 install --upgrade pip && \
    pip3 install python-keyczar docker-py && \
    SODIUM_INSTALL=system pip install pynacl && \
    pip3 install textfsm &&\
    \
    pip3 install --upgrade \
        jinja2 pycryptodome paramiko httplib2 &&\
    pip3 install ansible==${ANSIBLE_VERSION} && \
    pip3 install f5-sdk && \
    pip3 install boto && \
    pip3 install boto3 && \
    apk add libxml2-dev && \
    apk add libxslt-dev && \
    pip3 install napalm && \
    pip3 install pysftp && \
    pip3 install napalm-ansible && \
    pip3 install --upgrade python-gitlab

	# Clone Git repo
RUN git clone https://github.com/jhtut/acidipy.git &&\
    cd acidipy &&\
    python3 setup.py build &&\
    python3 setup.py install
	  
VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]
CMD ["/bin/bash"]
