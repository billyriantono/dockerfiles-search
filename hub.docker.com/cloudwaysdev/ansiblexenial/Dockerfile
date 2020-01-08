FROM ubuntu:16.04
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --no-install-recommends \
        openssh-server \
        apt-transport-https \
        ca-certificates \
        curl \
        file \
        htop \
        iproute2 \
        krb5-locales \
        libatm1 \
        libxtables11 \
        libsasl2-modules \
        locales \
        lsof \
        lsb-release \
        net-tools \
        openssl \
        python3 \
        python3.5 \
        python3-minimal \
        python3.5-minimal \
        tree \
        wget \
        unzip \
        vim \
        zip

RUN mkdir /var/run/sshd

RUN echo 'root:123' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/StrictModes yes/StrictModes no/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN mkdir /root/.ssh && touch authorized_keys /root/.ssh/
# Volume Configuration
VOLUME ["/root/.ssh"]

EXPOSE 80
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]