FROM nginx:latest
MAINTAINER fluendo


RUN apt-get update -y && \
    apt-get upgrade -y

ENV DEBIAN_FRONTEND noninteractive
RUN mkdir -p /usr/share/man/man1
#Install java sdk
RUN apt-get install -y wget software-properties-common openjdk-11-jdk

#Install hbbtv tools
RUN apt-get -y install php7.3-fpm php7.3-xml unionfs-fuse iproute2

#Set jenkins' configuration
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

ENV JENKINS_HOME /home/${user}

# Jenkins is run with user `jenkins`, uid = 1000
RUN groupadd -g ${gid} ${group} \
    && useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user}

RUN chown -R ${user}:${user} /home/${user}

# Add the jenkins user to sudoers
RUN echo "${user}    ALL=(ALL)    ALL" >> etc/sudoers


RUN mkdir /run/php && \
    touch /run/php/php7.3-fpm.sock

COPY www.conf /etc/php/7.3/fpm/pool.d/
RUN  rm /etc/php/7.3/fpm/conf.d/10-opcache.ini
EXPOSE 80

COPY run.sh .
CMD ["./run.sh"]