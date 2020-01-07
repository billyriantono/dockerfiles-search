FROM jenkins/jnlp-slave
USER root

WORKDIR /app

#RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
#RUN echo "LANG=en_US.UTF-8" >> /etc/environment
#RUN echo "NODE_ENV=development" >> /etc/environment
#RUN more "/etc/environment"
#RUN locale-gen en_US en_US.UTF-8
#RUN dpkg-reconfigure locales

#RUN apt-get update && \
#      apt-get -y install sudo
      
#RUN apt-get upgrade -y
#RUN apt-get dist-upgrade -y
#RUN apt-get install curl git ssh zip build-essential libssl-dev -y
RUN apt-get -y update && apt-get -y install --no-install-recommends git ssh
#RUN apt-get install curl git ssh -y

WORKDIR /root
RUN mkdir -p /root/.ssh
COPY keys /root/.ssh


RUN eval $(ssh-agent -s) && ssh-add /root/.ssh/git-cg-services-rsa
RUN ls /root/.ssh

#RUN ssh -vT git@github.com
RUN git clone ssh://git@github.com/eransc/cg-services.git

#RUN apt-get install curl htop git zip nano ncdu build-essential chrpath libssl-dev libxft-dev pkg-config glib2.0-dev libexpat1-dev gobject-introspection python-gi-dev apt-transport-https libgirepository1.0-dev libtiff5-dev libgsf-1-dev fail2ban nginx -y
#RUN apt-get install curl htop git zip nano ncdu build-essential chrpath libssl-dev libxft-dev pkg-config glib2.0-dev libexpat1-dev gobject-introspection python-gi-dev apt-transport-https libgirepository1.0-dev libtiff5-dev libjpeg-turbo8-dev libgsf-1-dev fail2ban nginx -y

# Install Node.js
#RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
#RUN apt-get install --yes nodejs
#RUN node -v
#RUN npm -v
#RUN npm i -g nodemon
#RUN nodemon -v

# Install Allure
#RUN wget https://github.com/allure-framework/allure1/releases/download/allure-core-1.5.2/allure-commandline.zip
#RUN unzip allure-commandline.zip -d /usr/local/bin/allure

# Cleanup
#RUN apt-get update && apt-get upgrade -y && apt-get autoremove -y
#ENTRYPOINT ["jenkins-slave"]
