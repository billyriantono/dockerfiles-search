FROM registry.centos.org/dharmit/base

LABEL RUN docker run -d -p 11300:11300 registry.centos.org/dharmit/beanstalkd:latest

RUN sudo yum -y update && \
    sudo yum -y install epel-release && \
    sudo yum -y install beanstalkd && \
    sudo yum clean all

EXPOSE 11300

CMD ["beanstalkd", "-p", "11300"]
