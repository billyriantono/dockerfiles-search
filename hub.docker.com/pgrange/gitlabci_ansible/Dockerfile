FROM gitlab/gitlab-runner

#Install ansible
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y dist-upgrade

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y locales python-pip python-dev \
                       git sudo aptitude vim \
                       libffi-dev libssl-dev curl \
                       net-tools
RUN pip install --upgrade PyYAML jinja2 paramiko ansible dnspython setuptools pyasn1
RUN mkdir /etc/ansible
COPY ansible.cfg /etc/ansible/ 

#Install docker
RUN DEBIAN_FRONTEND=noninteractive apt-get update &&\
    apt-get -y install apt-transport-https ca-certificates
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main">/etc/apt/sources.list.d/docker.list
RUN apt-get update &&\
    apt-get -y install docker-engine
