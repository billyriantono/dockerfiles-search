FROM ubuntu

RUN apt update -y && \
    apt install -y sudo vim netcat wget \
                   ca-certificates build-essential \
                   gawk texinfo pkg-config gettext automake libtool \
                   bison flex zlib1g-dev libgmp3-dev libmpfr-dev libmpc-dev \
                   git zip sshpass mc curl python expect bc telnet \
                   openssh-client tftpd-hpa libid3tag0-dev gperf libltdl-dev autopoint \
                   module-init-tools

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

CMD /bin/bash