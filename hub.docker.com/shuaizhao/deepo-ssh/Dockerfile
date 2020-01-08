FROM ufoym/deepo:all-py36-jupyter
MAINTAINER shuaizhao "zhaoyd14@outlook.com"

RUN apt-get update
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:deepossh' | chpasswd

EXPOSE 22 8888 6006
CMD ["/usr/sbin/sshd", "-D"]
