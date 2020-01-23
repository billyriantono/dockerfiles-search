FROM fedora:24
MAINTAINER Gerard Braad <me@gbraad.nl>

VOLUME /var/www
EXPOSE 80

RUN dnf install -y httpd; dnf clean all; systemctl enable httpd;
CMD ["/sbin/init"]
