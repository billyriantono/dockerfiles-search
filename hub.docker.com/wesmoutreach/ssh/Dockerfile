FROM ubuntu:14.04
MAINTAINER Wes McNamee <wes.mcnamee@outreach.io>

EXPOSE 22

LABEL io.outreach.version="0.1.1" \
      io.outreach.release-date="2017-02-13" \
      io.outreach.docker-hub-repo="wesmoutreach/ssh"

RUN apt-get update &&\
    apt-get install -y \
        openssh-server \
        python-setuptools &&\
    easy_install pip &&\
    python -m pip install --upgrade awscli &&\
    rm -rf /var/lib/apt/lists/* &&\
    mkdir /var/run/sshd &&\
    mkdir -p /root.ssh &&\
    sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config &&\
    sed -i 's/RSAAuthentication yes/RSAAuthentication no/' /etc/ssh/sshd_config

COPY docker_rsa.pub /root/.ssh/authorized_keys

CMD ["/usr/sbin/sshd", "-D"]
