FROM binhex/arch-base:latest
MAINTAINER John Peel <john@dgby.org>

ADD build/root/*.sh /root/

RUN chmod +x /root/*.sh && \
    /bin/bash /root/install.sh
