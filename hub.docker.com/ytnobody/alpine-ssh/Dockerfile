FROM ytnobody/alpine-perl:latest
MAINTAINER ytnobody <ytnobody@gmail.com>

RUN apk update && apk add openssh

RUN mkdir /root/.ssh
RUN echo $SSH_KEY > /root/.ssh/authorized_keys 

EXPOSE 22

CMD ["/usr/bin/sshd", "-D"]