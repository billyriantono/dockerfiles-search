FROM quin/fedora-systemd:latest
RUN dnf -y install httpd php; dnf clean all; systemctl enable httpd
EXPOSE 80
