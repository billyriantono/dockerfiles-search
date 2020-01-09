#
# Docker Ubuntu Java
#
# https://github.com/silviu-burcea/docker-ubuntu-java
#

FROM silviuburceadev/docker-ubuntu-base
MAINTAINER Silviu BURCEA (silviuburceadev@gmail.com)

# Install Java 8
run add-apt-repository -y ppa:webupd8team/java
run apt-get update
run echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
run apt-get install -y oracle-java8-installer

# Define default command.
CMD ["bash"]