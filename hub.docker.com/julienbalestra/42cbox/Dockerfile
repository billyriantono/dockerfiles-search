FROM debian:latest

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -y \
        build-essential \
        valgrind \
        git \
        python \
        libncurses5-dev && \
     apt-get clean autoclean && \
     apt-get autoremove -y

COPY shell_hook.sh /root/shell_hook.sh

ENTRYPOINT ["/root/shell_hook.sh"]