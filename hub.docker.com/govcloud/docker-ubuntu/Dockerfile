FROM govcloud/docker-ubuntu:systemd

LABEL maintainer "William Hearn <william.hearn@canada.ca>"

ENV DEBIAN_FRONTEND noninteractive

ENV PACKER_VERSION=1.2.0

RUN apt-get update && \
    apt-get install -y curl \
                       git \
                       jq \
                       qemu-utils \
                       unzip \
                       wget && \
    rm -rf /var/lib/apt/lists/*

# Install VirtualBox
RUN wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc -O- | apt-key add - && \
    sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian xenial contrib" >> /etc/apt/sources.list.d/virtualbox.list' && \
    apt-get update && \
    apt-get install -y linux-headers-azure \
                       virtualbox-5.2 || /bin/true && \
    rm -rf /var/lib/apt/lists/*

# Install Virtualbox Extension Pack
#RUN VBOX_VERSION=`dpkg -s virtualbox-5.2 | grep '^Version: ' | sed -e 's/Version: \([0-9\.]*\)\-.*/\1/'` ; \
#    wget http://download.virtualbox.org/virtualbox/${VBOX_VERSION}/Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack ; \
#    VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack ; \
#    rm Oracle_VM_VirtualBox_Extension_Pack-${VBOX_VERSION}.vbox-extpack

# Virtualbox driver device must be mounted from host
VOLUME /dev/vboxdrv

# Install Packer
#RUN curl -L -o packer_${PACKER_VERSION}_linux_amd64.zip https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip && \
#    curl -L -o packer_${PACKER_VERSION}_SHA256SUMS https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS && \
#    sed -i "/packer_${PACKER_VERSION}_linux_amd64.zip/!d" packer_${PACKER_VERSION}_SHA256SUMS && \
#    sha256sum -c packer_${PACKER_VERSION}_SHA256SUMS && \
#    unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin && \
#    rm -f packer_${PACKER_VERSION}_linux_amd64.zip

# Install Packer (ansible-local fix)
RUN curl -L -o packer_${PACKER_VERSION}_linux_amd64.zip https://github.com/hashicorp/packer/files/1729632/packer.zip && \
    unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin && \
    rm -f packer_${PACKER_VERSION}_linux_amd64.zip
