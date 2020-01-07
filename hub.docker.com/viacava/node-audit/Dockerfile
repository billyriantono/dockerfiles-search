ARG NODE_VERSION=12.10.0-alpine
ARG BUILD_DATE
ARG VERSION
FROM node:${NODE_VERSION}
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.URL="https://github.com/viacava/node-audit" \
      org.label-schema.node=$NODE_VERSION \
      org.label-schema.version=$VERSION \
      maintainer="https://github.com/viacava"
WORKDIR /opt/audit
COPY ./src .
RUN chmod 775 /opt/audit/entrypoint.sh
ENTRYPOINT [ "/opt/audit/entrypoint.sh" ]
CMD ["--run"]
