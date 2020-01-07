FROM       valian/docker-python-opencv-ffmpeg:py3
MAINTAINER zlong "jidebingfeng@126.com"


RUN echo $http_proxy && \
    echo $https_proxy && \

    apt-get -y update && \

#### tools
    apt-get install -y openssh-server net-tools iputils-ping curl wget vim proxychains sudo && \
    mkdir /var/run/sshd && \

    echo 'root:root' |chpasswd && \

    sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \


# config proxychains
    sed -ri 's/socks4/#socks4/g' /etc/proxychains.conf && \
    echo socks5  127.0.0.1 1080 >> /etc/proxychains.conf


EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
