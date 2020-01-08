#
# docker run -p 8080:8080 -p 50000:50000 \
#   -v /data/jenkins:/var/jenkins \
#   --restart always \
#   --name jenkins
#

FROM ubuntu:trusty
MAINTAINER Faissal bibelghach <glfaissal@gmail.com>

#ENV JENKINS_HOME /var/jenkins
ENV JENKINS_HOME /var/jenkins_home
ENV JENKINS_OPTS ""
ENV JENKINS_VERSION "2.46.2"

WORKDIR /opt
# RUN apk add --update git openjdk8-jre ttf-dejavu \
#     && rm -rf /var/cache/apk/* \
#     && wget http://mirrors.jenkins.io/war-stable/${JENKINS_VERSION}/jenkins.war
RUN apt-get update && apt-get install -y software-properties-common  debconf-utils && \
	add-apt-repository ppa:webupd8team/java -y  && \
	apt-get update && \
	echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" |  debconf-set-selections && \
	apt-get install -qqy \
	oracle-java8-installer ttf-dejavu oracle-java8-set-default \
	apt-transport-https curl python-dev python-setuptools gcc make libssl-dev git -y && \
    easy_install pip && \
	wget http://mirrors.jenkins.io/war-stable/${JENKINS_VERSION}/jenkins.war && \
	echo 'jenkins ALL=(ALL) NOPASSWD: /usr/local/bin/docker' >> /etc/sudoers 

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && \
    echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | tee /etc/apt/sources.list.d/docker.list && \
    apt-get update -y && \
    apt-get purge lxc-docker* -y && \
    apt-get install docker-engine -y

RUN pip install docker-compose && \
    pip install ansible boto boto3


VOLUME  ${JENKINS_HOME}
EXPOSE 8080
EXPOSE 50000

CMD ["java", "-jar", "/opt/jenkins.war", "$JENKINS_OPTS"]