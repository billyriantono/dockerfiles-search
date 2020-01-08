FROM maven:3-jdk-8

MAINTAINER 1000kit <docker@1000kit.org>

LABEL Vendor="1000kit" \
      License=GPLv3 \
      Version=1.0.0

ADD init/* /opt/

RUN apt-get update  \
   && apt-get -y install gettext-base \
   && apt-get clean
   
ENTRYPOINT ["/opt/entrypoint.sh"]

#END
