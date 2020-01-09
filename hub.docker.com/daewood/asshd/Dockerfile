FROM daewood/abase

MAINTAINER daewood <daewood@qq.com>

RUN apk --update add openssh \
  && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
  && echo "root:root" | chpasswd \
  && rm -rf /var/cache/apk/* \
  && ssh-keygen -A
  
COPY rootfs/ /

WORKDIR /root
EXPOSE 22
ENTRYPOINT ["/init"]

