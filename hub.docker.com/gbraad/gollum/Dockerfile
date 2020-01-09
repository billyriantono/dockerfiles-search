FROM registry.gitlab.com/gbraad/fedora:24
MAINTAINER Gerard Braad <me@gbraad.nl>

RUN dnf install -y ruby libicu git ; \
    dnf install -y ruby-devel @development-tools @rpm-development-tools @c-development libicu-devel zlib-devel ; \
    gem install gollum --no-ri --no-rdoc ; \
    dnf history -y undo 3 ; \
    dnf clean all ; \
    mkdir -p /workspace

EXPOSE 4567

VOLUME /workspace
WORKDIR /workspace

CMD gollum
