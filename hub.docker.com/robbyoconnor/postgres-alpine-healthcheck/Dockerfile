FROM postgres:alpine
LABEL maintainer="Robby O'Connor <robby.oconnor@gmail.com>"
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/robbyoconnor/postgres-alpine-healthcheck.git" \
      org.label-schema.vcs-ref=$VCS_REF
COPY docker-healthcheck /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-healthcheck
HEALTHCHECK CMD ["/usr/local/bin/docker-healthcheck"]
