FROM docker:dind
MAINTAINER seltmann@ub.uni-leipzig.de
VOLUME [ "/home/docker", "/jenkins" ]
CMD ["/start.sh"]
ADD start.sh slave.jar /
RUN apk update \
 && apk add openjdk8-jre-base git openssh \
 && rm /var/cache/apk/* \
 && adduser -H -D docker \
 && chmod a+x /start.sh \
 && chmod 644 /slave.jar