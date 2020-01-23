FROM postgres:10-alpine

RUN apk add --no-cache openssh \
  && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
  && echo "root:changeme" | chpasswd \
  && ssh-keygen -A

EXPOSE 22

