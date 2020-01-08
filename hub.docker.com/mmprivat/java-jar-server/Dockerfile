FROM openjdk:9-jre-slim
LABEL "MAINTAINER" "Manuel Manhart <manuel@manhart.space>"
# Generic image parts
ADD content/scripts/ /scripts/
ADD IMAGE_NAME /
ADD IMAGE_VERSION /
ENV LOG=/var/log/container.log

# specific image parts
WORKDIR /jar

ENTRYPOINT ["/scripts/start.sh"]

HEALTHCHECK --interval=30s --timeout=3s \
  CMD /scripts/healthcheck.sh || exit 1