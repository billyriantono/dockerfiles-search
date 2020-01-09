FROM kalilinux/kali-linux-docker:latest

LABEL mantainer="qiyingwangwqy@gmail.com"

RUN apt-get -y update && \
    apt-get -y install --fix-missing kali-linux-full && \
    apt-get -y install --fix-missing locales-all xfce4 xfce4-terminal vnc4server tightvncserver -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "root:root" | chpasswd  && \
    echo “xfce4-session” >~/.xsession && \
    printf 'export LANG=zh_CN\n\
export LANGUAGE=zh_CN.UTF-8\n\
export LC_ALL=zh_CN.UTF-8\n' >> /etc/environment

EXPOSE 3350
EXPOSE 3389

CMD ['/bin/cat']