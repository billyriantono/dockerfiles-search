FROM mrlshjjang/django-server
MAINTAINER mrlshjjang <mrlshjjang@gmail.com>
RUN (echo "deb http://archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse" > /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse" >> /etc/apt/sources.list)

ADD . /jenkins_home/

# jenkin install
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
RUN sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update
RUN sudo apt-get install -y jenkins

# env config
VOLUME /jenkins_home
ENV JENKINS_HOME /jenkins_home

# for main web interface:
# will be used by attached slave agents:
EXPOSE 8080 50000

CMD ["/jenkins_home/run.sh"]
