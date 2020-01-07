FROM alpine
# Uncomment if you are going to build on a raspberry pi
# FROM armhf/alpine

RUN apk --no-cache --update add bash wget openssh curl git && rm -rf /tmp/* /var/cache/apk/*

ADD docker-entrypoint.sh /

# Make sure we get fresh keys
RUN rm -rf /etc/ssh/ssh_host_rsa_key /etc/ssh/ssh_host_dsa_key
RUN chmod 775 /docker-entrypoint.sh

EXPOSE 22
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/usr/sbin/sshd", "-D"]
