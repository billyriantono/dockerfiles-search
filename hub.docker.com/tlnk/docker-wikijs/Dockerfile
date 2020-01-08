#Dockerfile docker-wikijs
FROM requarks/wiki:latest
LABEL maintainer="tlnk.fr"

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

EXPOSE 80

WORKDIR /var/wiki
COPY entrypoint /entrypoint

RUN apk update && \
    apk add nano --no-cache && \
    chmod +x /entrypoint/*sh && \
    chmod +x /entrypoint/entrypoint.d/*.sh

ENTRYPOINT ["/bin/bash", "/entrypoint/entrypoint.sh"]
CMD ["node", "server"]


LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/tle06/docker-wikijs.git"
LABEL org.label-schema.name="docker-wikijs"
LABEL org.label-schema.vendor="docker-wikijs"
LABEL org.label-schema.schema-version="1.0"
