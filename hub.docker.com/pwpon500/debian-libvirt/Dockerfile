FROM pwpon500/debian-systemd

RUN apt update && apt install qemu-kvm libvirt-clients libvirt-daemon-system -y && apt clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN systemctl enable libvirtd

RUN ln -s /etc/libvirt/qemu/networks/default.xml /etc/libvirt/qemu/networks/autostart/default.xml
