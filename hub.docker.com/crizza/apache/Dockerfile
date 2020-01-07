FROM crizza/ubuntu

ARG SHELL=$SHELL
ARG DOCKER_USER=$DOCKER_USER
ARG DOCKER_GROUP=$DOCKER_GROUP

ENV SHELL $SHELL

COPY z-default.conf /etc/apache2/sites-available/z-default.conf
COPY switcher.sh /opt/switcher.sh
COPY setup.sh /opt/setup.sh
RUN /bin/bash /opt/setup.sh

USER $DOCKER_USER

# Star services and keep them alive
COPY startup.sh /opt/startup.sh
CMD bash /opt/startup.sh
