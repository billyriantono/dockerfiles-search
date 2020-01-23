FROM ubuntu:14.04
MAINTAINER Alien4Cloud Development Team <alien4cloud@fastconnect.fr>

#Add Oracle JDK repo to the source lists
#Accept automatically the oracle licence
ADD webupd8team-java.list /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true \
    | /usr/bin/debconf-set-selections

# Installing prerequisites
RUN apt-get update && apt-get install -y \
  wget \
  git \
  maven \
  npm \
  oracle-java7-installer \
  oracle-java7-set-default \
  python \
  ruby \
  ruby-dev \
  xvfb

# Upstart and DBus have issues inside docker. We work around in order to install firefox.
RUN dpkg-divert --local --rename --add /sbin/initctl && \
    ln -sf /bin/true /sbin/initct

# Set locale (fix the locale warnings)
RUN localedef -v -c -i en_US -f UTF-8 en_US.UTF-8 || :

# Set locale to en_US
ADD default_locale /etc/default/locale
RUN echo 'Acquire::Languages {"none";};' > /etc/apt/apt.conf.d/60language && \
    locale-gen en_US.UTF-8 && \
    update-locale en_US.UTF-8

# Install gem deps
RUN gem install --no-ri --no-rdoc compass

# Download & install go agent
RUN cd /tmp && \
    wget -nc -nv http://download.go.cd/gocd-deb/go-agent-14.4.0-1356.deb && \
    dpkg -i -E /tmp/go-agent-14.4.0-1356.deb

# Avoids EACCES error when you try to install a package globally
RUN mkdir /.npm /.config /.local /.bower && \
    chown -R go /.npm /.config /.local /.bower /usr/local

# Copy go agent conf file
# remember to change the go server address
ADD go-agent /etc/default/go-agent

# Auto-approve new agents
ADD autoregister.properties /var/lib/go-agent/config/autoregister.properties

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add a symbolic link node -> nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node

# Add FastConnect certificate to keystore
ADD http://fastconnect.org/ssl/cacert.crt /usr/share/ca-certificates/fastconnect.crt
RUN chmod 644 /usr/share/ca-certificates/fastconnect.crt
RUN keytool -keystore $(readlink -f /usr/bin/java | sed "s:bin/java::")/lib/security/cacerts -import -alias fastconnect -file /usr/share/ca-certificates/fastconnect.crt -storepass changeit -noprompt

# Start the go agent service and keep the container running
CMD /usr/share/go-agent/agent.sh && tail -F /var/log/go-agent/go-agent.log &
