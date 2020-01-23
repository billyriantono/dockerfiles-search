FROM debian:stretch-slim
RUN apt-get update && \
    apt-get install -y openssh-server && \
    mkdir /run/sshd && \
    echo PasswordAuthentication no >> /etc/ssh/sshd_config
CMD ["/usr/sbin/sshd", "-e", "-D"]
