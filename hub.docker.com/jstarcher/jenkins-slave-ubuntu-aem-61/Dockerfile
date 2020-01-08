# Pull base image.
FROM ubuntu

# Install Java.
RUN \
  apt-get install -y software-properties-common && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Install Maven3
RUN \ 
  apt-add-repository -y ppa:andrei-pozolotin/maven3 && \
  apt-get update && \
  apt-get install -y maven3

# Install git
RUN apt-get install -y git

# Install Grunt
RUN \
 apt-get install -y nodejs && \
 apt-get install -y npm && \
 npm install -g bower && \
 npm install -g grunt-cli


# Install a basic SSH server
RUN apt-get install -y openssh-server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Add user jenkins to the image
RUN adduser --quiet jenkins

# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd
RUN echo "jenkins   ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers.d/jenkins
RUN sed -ri 's/Defaults    requiretty/#Defaults    requiretty/g' /etc/sudoers

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]