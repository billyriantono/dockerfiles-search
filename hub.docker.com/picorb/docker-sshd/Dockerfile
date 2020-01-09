# Pull base image.
FROM dockerfile/python

# Install Ansible.
RUN pip install ansible

# Define working directory.
WORKDIR /data

# MAINTAINER Francesco Sullo, sullof@sullof.com, http://sullof.com
# Let's start with some basic stuff.
RUN apt-get update -qq && apt-get -y upgrade && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    lxc \
    iptables \
    openssh-server python-setuptools && /usr/bin/easy_install supervisor
    
# Install Docker from Docker Inc. repositories.
RUN curl -sSL https://get.docker.com/ubuntu/ | sh

# Install the magic wrapper.
ADD ./wrapdocker /usr/local/bin/wrapdocker
RUN chmod +x /usr/local/bin/wrapdocker

# Define additional metadata for our image.
VOLUME /var/lib/docker

#ADD adds/authorized_keys /authorized_keys
RUN curl https://gist.githubusercontent.com/ericson-cepeda/747c7a67f26db36e7433/raw/authorized_keys -o /authorized_keys
ADD adds/configure.sh /configure.sh
RUN bash /configure.sh && rm /configure.sh

ADD adds/supervisord.conf /etc/supervisord.conf

EXPOSE 22

CMD ["bash", "-c", "wrapdocker && /usr/local/bin/supervisord -n"]

