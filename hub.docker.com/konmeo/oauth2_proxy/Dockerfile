FROM konmeo/alpine

MAINTAINER konmeo

EXPOSE 4180

COPY bin/${EXEC} /usr/local/bin/

USER nobody
ENTRYPOINT ["oauth2_proxy"]
