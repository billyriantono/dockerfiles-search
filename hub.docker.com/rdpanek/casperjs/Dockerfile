# A image with casperjs 1.1-beta3 ( master branch )
# For more information; https://github.com/rdpanek/docker_casperjs

FROM rdpanek/phantomjs:2.0.0
MAINTAINER Radim Daniel Pánek <rdpanek@gmail.com>


# Commands
RUN \
  mkdir -p /srv/var && \
  git clone https://github.com/rdpanek/casperjs /srv/var/casperjs && \
  cd /srv/var/casperjs && \
  git ch -b develop  &&  git pull origin develop && \
  git l -10 --no-color && \
  ln -s /srv/var/casperjs/bin/casperjs /usr/bin/casperjs

# Default command
CMD ["/usr/bin/casperjs"]
