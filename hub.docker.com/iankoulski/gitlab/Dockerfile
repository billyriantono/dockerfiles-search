FROM gitlab/gitlab-ce:12.5.2-ce.0

MAINTAINER Alex Iankoulski <alex_iankoulski@yahoo.com>

ARG http_proxy
ARG https_proxy
ARG no_proxy

ADD Container-Root /

RUN export http_proxy=$http_proxy; export https_proxy=$https_proxy; export no_proxy=$no_proxy; /setup.sh; rm -f /setup.sh

CMD /startup.sh

