FROM gitlab/gitlab-runner:latest
MAINTAINER toch

# Install VirtualBox
RUN echo "deb http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" >> /etc/apt/sources.list.d/virtualbox.list
RUN wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | apt-key add -
RUN apt-get update && apt-get install -y --no-install-recommends \
  virtualbox-5.0

# Install Vagrant
RUN wget https://releases.hashicorp.com/vagrant/1.8.1/vagrant_1.8.1_x86_64.deb \
  && dpkg -i vagrant_1.8.1_x86_64.deb
