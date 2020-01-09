#
# thumbor image
#

FROM apsl/thumbor:6.6.0

ENV NAME="unite thumbor" \
    SUMMARY="unite thumbor" \
    DESCRIPTION="unite thumbor"

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="${NAME}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="${NAME}" \
      name="unitecms/docker-thumbor" \
      version="1.0" \
      maintainer="www.unitecms.io <stefan@unite.co.at>"

USER root

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install nginx && \
    apt-get -y install supervisor

COPY ./root/ /

RUN container-setup

EXPOSE 8080

USER 1001

ENTRYPOINT ["docker-entrypoint"]
CMD ["supervisord", "-n"]