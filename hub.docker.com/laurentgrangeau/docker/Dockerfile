FROM anapsix/alpine-java:jre8

MAINTAINER Chritophe Lecointe <christophe.lecointe@tuta.io>

RUN apk upgrade --update && apk add wget unzip

ENV version 5.1.4
RUN wget -q https://dist.xebialabs.com/public/trial/xl-deploy/xl-deploy-${version}-server-trial-edition.zip -O /tmp/xld.zip && \
    unzip -q /tmp/xld.zip -d /opt && \
    rm /tmp/xld.zip
ADD xldeploy.answers /opt/xl-deploy-${version}-server-trial-edition/bin/xldeploy.answers

WORKDIR /opt/xl-deploy-${version}-server-trial-edition/bin
RUN ["./run.sh", "-setup", "-reinitialize", "-force", "-setup-defaults", "./bin/xldeploy.answers"]

VOLUME /opt/xl-deploy-${version}-server-trial-edition/conf
VOLUME /opt/xl-deploy-${version}-server-trial-edition/ext
VOLUME /opt/xl-deploy-${version}-server-trial-edition/hotfix
VOLUME /opt/xl-deploy-${version}-server-trial-edition/importablePackages
VOLUME /opt/xl-deploy-${version}-server-trial-edition/log
VOLUME /opt/xl-deploy-${version}-server-trial-edition/plugins
VOLUME /opt/xl-deploy-${version}-server-trial-edition/repository

EXPOSE 4516

CMD ["./run.sh"]
