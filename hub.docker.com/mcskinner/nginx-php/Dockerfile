# Start from the base NGINX image.
FROM mcskinner/nginx
MAINTAINER Michael Skinner <git@mcskinner.com>

# Install php-fpm and a few additional requirements.
RUN apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install php5-fpm php5-mysql php-apc python-setuptools

# Fix up the default php-fpm config in two important ways:
#  (1) Disallow automatic path rewrites, which closes a huge security hole.
#  (2) Don't run as a daemon inside the container.
RUN sed -i -e "s/;cgi.fix_pathinfo\s*=\s*1/cgi.fix_pathinfo = 0/g" /etc/php5/fpm/php.ini && \
  sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf

# Install Supervisor and feed it our config to run php-fpm and nginx side by side.
RUN /usr/bin/easy_install supervisor
RUN /usr/bin/easy_install supervisor-stdout
ADD ./supervisord.conf /etc/supervisord.conf

# Seems like Supervisor can piss Upstart off.
# We take Supervisor's side and just keep Upstart from complaining.
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# Spin up our Supervisor setup by default.
CMD ["/usr/local/bin/supervisord", "-n", "-c", "/etc/supervisord.conf"]
