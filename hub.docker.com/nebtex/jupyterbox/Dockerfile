# Build as jupyterhub/singleuser
# Run with the DockerSpawner in JupyterHub

FROM nebtex/python-base:machine-learning

MAINTAINER Nebular Vortex <publicdev@nebtex.com>

EXPOSE 8888
EXPOSE 7070
ADD singleuser.sh /srv/singleuser/singleuser.sh
RUN chmod +x /srv/singleuser/singleuser.sh

ADD docker-entrypoint.sh /srv/singleuser/docker-entrypoint.sh
RUN chmod +x /srv/singleuser/docker-entrypoint.sh

ADD boostrap.sh /srv/singleuser/boostrap.sh
RUN chmod +x /srv/singleuser/boostrap.sh

ADD supervisord.conf /etc/
RUN mkdir -p /usr/local/etc/haproxy/
ADD haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

WORKDIR /root
ENV HOME=/root

CMD ["/srv/singleuser/boostrap.sh"]

