FROM jenkins:latest

USER root
RUN apt-get update && apt-get install -y qemu-kvm qemu virt-manager virt-viewer libvirt-daemon-system libvirt-dev libvirt-clients && rm -rf /var/lib/apt/lists/*
USER jenkins
