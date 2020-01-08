# Specifing the base image
FROM            ubuntu:14.04.3

# Maintainer
MAINTAINER      "Vaibhav Todi"       <vaibhavtodi1989@gmail.com>

# Specifing the Label
LABEL    Description="A MongoDB Docker image where base image is Ubuntu 14.04.3"            \
         Version="1.0"

# Setting the Environment & Working Directory
ENV      home       /root
WORKDIR  $home
USER     root

# Updating the base system & installing the packages
RUN      apt-get  update                                                                                                      \
     &&  apt-get  install  -y   apt-transport-https software-properties-common vim

# Importing, Downloading & Insatalling MongoDB.org
RUN      apt-key  adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927                                               \
     &&  echo     "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list   \
     &&  apt-get  update                                                                                                      \
     &&  apt-get  install  -y   mongodb-org

# Copy entrypoint.sh script
COPY     entrypoint.sh   /entrypoint.sh

# Cleaning the Docker Image
RUN      apt-get   -y    clean                                                                                               \
     &&  rm        -rf   /var/lib/apt/lists/*                                                                                \
     &&  rm        -rf   /var/cache/*

# Exposing the port
EXPOSE   27017

# Mounting the Volume
VOLUME   ["/var/log/mongodb", "/var/lib/mongodb"]

# CMD Insstruction
CMD      ["/entrypoint.sh"]
