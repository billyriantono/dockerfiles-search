FROM dclong/ubuntu_b

RUN /scripts/create_user_nogroup.sh linuxbrew 1001

USER linuxbrew
WORKDIR /home/linuxbrew
RUN git clone https://github.com/Linuxbrew/brew.git /home/linuxbrew/.linuxbrew

ENV PATH=/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH \
    SHELL=/bin/bash

