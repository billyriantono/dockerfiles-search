FROM oraclelinux:6
MAINTAINER henrik@hedlund.im

RUN yum upgrade -y

# fix locale error
RUN echo LANG=en_US.utf-8 >> /etc/environment \
 && echo LC_ALL=en_US.utf-8 >> /etc/environment \
 && echo LANGUAGE=en_US.utf-8 >> /etc/environment

# Set the timezone
RUN echo "Europe/Oslo" > /etc/timezone
