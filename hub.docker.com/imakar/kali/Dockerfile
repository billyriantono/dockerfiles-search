FROM kalilinux/kali-linux-docker
LABEL MAINTAINER="m2kar <m2kar.cn@gmail.com>"

RUN apt-get update && \
    apt-get install -y -q openssh-server git curl zsh kali-defaults kali-tools-top10  && \
    rm -rf /var/lib/apt/lists/*

RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh) --unattended" && \
    chsh -s /bin/zsh
# remove comment of the following line to install custome packet
# RUN apt-get update && \  
#    apt-get install -y -q kali-linux && \
#    apt-get install -y -q kali-linux-forensic && \
#    apt-get install -y -q kali-linux-full && \
#    apt-get install -y -q kali-linux-gpu && \
#    apt-get install -y -q kali-linux-pwtools && \
#    apt-get install -y -q kali-linux-rfid && \
#    apt-get install -y -q kali-linux-sdr && \
#    apt-get install -y -q kali-linux-top10 && \
#    apt-get install -y -q kali-linux-voip && \
#    apt-get install -y -q kali-linux-web && \
#    apt-get install -y -q kali-linux-wireless && \
 
VOLUME /data
ENV SSHD_PORT=22 PUBLIC_KEY=
COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh / # backwards compat
ENTRYPOINT ["/docker-entrypoint.sh"]
WORKDIR /data
CMD ["postgres"]
