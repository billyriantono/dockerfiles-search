#####
FROM nginx:1.16.0-alpine
MAINTAINER "telus/dockerfiles"

# paths #
ENV DEFAULT_DIR "/app"
ENV DEFAULT_USER "nginx"
ENV BINPATH "/usr/local/bin"
ENV PATH "$DEFAULT_DIR/bin:$PATH"
ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1
ENV SERVER_NAME "localhost"
RUN mkdir -p "$DEFAULT_DIR" ;
WORKDIR "$DEFAULT_DIR"

# install #
RUN apk add --update \
  "ca-certificates" \
  "gettext" \
  ;
COPY ./bin/* $BINPATH/
RUN chown -R "$DEFAULT_USER:$DEFAULT_USER" "$DEFAULT_DIR" ;
RUN rm -rf /var/cache/apk/* ;

# start #
EXPOSE 443
# USER $DEFAULT_USER
ENTRYPOINT [ "entry" ]
CMD nginx -g 'daemon off ;' ;
