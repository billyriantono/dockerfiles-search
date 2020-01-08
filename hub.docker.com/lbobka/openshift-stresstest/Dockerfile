FROM ubuntu:trusty
MAINTAINER Lars Bobka <lars.bobka@gmail.com>

RUN apt-get update && apt-get install -y stress 

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh / # backwards compat

USER 1001
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["--cpu", "1"]
