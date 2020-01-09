FROM hashicorp/packer:light
ENV PLUGIN_VERSION=2.0

ADD https://github.com/jetbrains-infra/packer-builder-vsphere/releases/download/v$PLUGIN_VERSION/packer-builder-vsphere-clone.linux /bin 
CMD chmod +x /bin/packer-builder-vsphere-clone.linux
