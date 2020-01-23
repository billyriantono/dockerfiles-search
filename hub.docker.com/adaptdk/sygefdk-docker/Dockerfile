#############################################################
# adamoss/docker-tcpdump DOCKER IMAGE
#
# RUN WITH docker run -it --net=host adamoss/docker-tcpdump
# 
# FOLLOW @sec_kc
############################################################
FROM alpine:latest
RUN apk update && apk add -y tcpdump
ENTRYPOINT ["/usr/sbin/tcpdump"]
#ENTRYPOINT ["/bin/sh"]
