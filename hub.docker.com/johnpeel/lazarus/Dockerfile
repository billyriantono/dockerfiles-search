FROM johnpeel/fpc:latest
MAINTAINER John Peel <john@dgby.org>

ADD build/root/*.sh /root/

ADD config/nobody/ /home/nobody/

RUN chmod +x /root/*.sh && \
    /bin/bash /root/install.sh
