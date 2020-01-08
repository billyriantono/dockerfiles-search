FROM fedora:23

MAINTAINER "Daniel Whatmuff" <danielwhatmuff@gmail.com>

RUN dnf upgrade -y -q && \ 
    dnf clean all && \
    dnf install -y -q python3 curl groff && \
    dnf clean all && \
    curl https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py && \
    python3 /tmp/get-pip.py && \
    pip install awscli && \
    rm -rf /root/.cache/pip && \
    mkdir -p /root/.aws && \
    aws --version

CMD ["aws"]
