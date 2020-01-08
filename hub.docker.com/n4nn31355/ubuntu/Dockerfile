FROM ubuntu:xenial

RUN apt-get update && \
    apt-get install sudo && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ONBUILD ARG USERNAME=custom
ONBUILD ARG UID=1000
ONBUILD ARG GID=1000

ONBUILD RUN groupadd -f -g ${GID} ${USERNAME} && \
    useradd -u ${UID} -g ${GID} -m ${USERNAME} && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
ONBUILD ENV CUSTOMUSER ${USERNAME} 
ONBUILD ENV HOME /home/${USERNAME} 
ONBUILD USER ${USERNAME} 
