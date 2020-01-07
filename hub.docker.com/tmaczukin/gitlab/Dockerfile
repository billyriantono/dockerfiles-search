FROM sameersbn/gitlab:7.13.3
MAINTAINER Tomasz Maczukin "tomasz@maczukin.pl"

RUN apt-get update && apt-get install -y patch && apt-get clean # update_20150806232733

ADD gitlab.patch /tmp/gitlab.patch

USER git
RUN cd /home/git/gitlab && patch -p 1 -i /tmp/gitlab.patch
USER root
