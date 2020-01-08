FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends git gitweb apache2 curl && rm --recursive --force /var/lib/apt/lists/*

# enable modules
RUN a2enmod cgi alias env rewrite auth_digest
RUN mkdir /opt/git

ADD git/git.conf /etc/apache2/conf-enabled/git.conf
# htdigest -c htpasswd "git repository" tatsuyasen
RUN echo "\$projectroot = \"/opt/git\";" > /etc/gitweb.conf && \
echo "\$git_temp = \"/tmp\";" >> /etc/gitweb.conf && \
echo "@diff_opts = ();" >> /etc/gitweb.conf

VOLUME ["/opt/git/"]
EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
# ENTRYPOINT ["/etc/samba/samba.sh"]
