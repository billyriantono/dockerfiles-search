#####
FROM vault:1.1.2
MAINTAINER "telus/dockerfiles"

# paths #
ENV DEFAULT_DIR "/vault"
ENV DEFAULT_USER "vault"
ENV BINPATH "/usr/local/bin"
ENV PATH "$DEFAULT_DIR/bin:$PATH"
ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV GOOGLE_APPLICATION_CREDENTIALS "/etc/google/auth/application_default_credentials.json"
RUN mkdir -p "/etc/google/auth" ;
RUN mkdir -p "$DEFAULT_DIR" ;
WORKDIR "$DEFAULT_DIR"

# install #
RUN apk add --update \
  "ca-certificates" \
  "gettext" \
  ;
COPY ./bin/* $BINPATH/
RUN mkdir -p "$DEFAULT_DIR/audit" ;
RUN chown -R "$DEFAULT_USER:$DEFAULT_USER" "$DEFAULT_DIR" ;
RUN rm -rf /var/cache/apk/* ;

# start #
EXPOSE 8200
ENTRYPOINT [ "entry" ]
CMD vault server -config "$DEFAULT_DIR/config" ;
