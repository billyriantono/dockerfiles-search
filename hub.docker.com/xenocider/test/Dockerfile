## xenocider/test:latest
FROM alpine:3.8
# FROM xenocider/test:sshd


# RUN apk add wget -U
# RUN wget -P /opt https://download.sysinternals.com/files/SysinternalsSuite.zip

# RUN ssh -p 20022 -fNR 10022:127.0.0.1:22 root@xenos.nsupdate.info \
    # && /usr/sbin/sshd -D

ADD https://vagrantcloud.com/generic/boxes/alpine38/versions/1.8.38/providers/virtualbox.box /opt
    
ADD test.sh /test.sh
RUN chmod +x /test.sh

CMD ["/bin/sh"]

# ssh-keygen -t rsa -P '' -f /root/.ssh/id_rsa
