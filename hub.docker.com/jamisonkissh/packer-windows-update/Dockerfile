FROM hashicorp/packer:light

RUN mkdir -p /tmp/windows-update && \
    wget https://github.com/rgl/packer-provisioner-windows-update/releases/download/v0.5.1/packer-provisioner-windows-update-linux.tgz -P /tmp/windows-update && \
    cd /tmp/windows-update && tar -xzvf packer-provisioner-windows-update-linux.tgz && mv packer-provisioner-windows-update /bin/ && \
    chmod 755 /bin/packer-provisioner-windows-update && chown root:root /bin/packer-provisioner-windows-update && \
    rm -rf /tmp/windows-update

ENTRYPOINT ["bin/packer"]
