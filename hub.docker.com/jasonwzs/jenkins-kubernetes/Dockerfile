FROM jenkins:latest
MAINTAINER Jason Wen <zhenshan.wen@gmail.com>

ARG EXTRA_PLUGINS="cloudbees-folder credentials-binding workflow-aggregator pipeline-stage-view git github mailer"

RUN /usr/local/bin/install-plugins.sh $EXTRA_PLUGINS kubernetes