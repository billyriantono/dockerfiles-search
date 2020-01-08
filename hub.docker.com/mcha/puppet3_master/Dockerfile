#
# Create an image with Puppet within
#
# @author : Michel CHA
FROM debian

WORKDIR /root

#ENV VARNAME value

# Shell form to run command -> will interpret variable defined with ENV
# RUN execute the command in a new layer -> recommended for tool installation
# Multiple RUN is possible
# Avoid the use of ADD => unpredictable

# Update packages
RUN apt-get update \
    && apt-get -y install wget inotify-tools vim locales locate ntp

# Compile locale
COPY resources/etc/locale.gen /etc/locale.gen
RUN locale-gen en_US.utf8 && locale-gen fr_FR.utf8

# Setup NTP
COPY resources/etc/ntp.conf /etc/ntp.conf
RUN service ntp restart

# Install Puppet
# Apache2 + mod_passenger (enable executing ruby/rails code)
# Several installation packages available, but this one is an interesting bundle
RUN apt-get -y install ca-certificates \
    && wget https://apt.puppetlabs.com/puppetlabs-release-jessie.deb \
    && dpkg -i puppetlabs-release-jessie.deb \
    && apt-get update \
    && apt-get -y install puppetmaster-passenger \
    && service apache2 stop
RUN rm -f puppetlabs-release-jessie.deb

# Puppet custom conf
COPY resources/etc/puppet /etc/puppet
COPY resources/etc/apache2/sites-enabled /etc/apache2/sites-enabled

# Stick Puppet version
COPY resources/etc/apt/preferences.d /etc/apt/preferences.d
COPY resources/stick_puppet_version.sh /root/stick_puppet_version.sh
RUN chmod u+x /root/stick_puppet_version.sh
RUN /root/stick_puppet_version.sh

# Setup to be finished inside running container
COPY resources/setup_cert.sh /root/setup_cert.sh
COPY resources/services.sh /root/services.sh
COPY resources/start.sh /root/start.sh

RUN chmod u+x /root/setup_cert.sh /root/services.sh /root/start.sh

# Other resources
COPY resources/.bashrc /root/.bashrc

# Exec form to run command -> will not interpret variable defined with ENV
# Exec form is recommanded for CMD and ENTRYPOINT
# CMD is used to specify a default command to run
# Will be overidden by the one provided on the docker run command line if any
CMD ["/root/start.sh"]

# When CMD is mixed with ENTRYPOINT
# Then CMD's value provide the args to the command in ENTRYPOINT
# This ensure a parameterized ENTRYPOINT
# Ex : docker run image_alias yyy
# will result in xxx yyy
#ENTRYPOINT ["xxx"]
