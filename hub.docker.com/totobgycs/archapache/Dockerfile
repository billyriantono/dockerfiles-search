FROM totobgycs/archdev
MAINTAINER totobgycs

USER build
RUN yaourt -Syy ; \
  yaourt -S --noconfirm apache ; \
  yes | yaourt -Scc
USER root
RUN echo "ServerName archapache" >> /etc/httpd/conf/httpd.conf ; \
  echo "archapache" > /srv/http/index.html ; \
  mkdir /var/run/httpd

VOLUME /var/www /srv/http
  
EXPOSE 80/tcp

ENTRYPOINT ["httpd", "-D", "FOREGROUND"]
