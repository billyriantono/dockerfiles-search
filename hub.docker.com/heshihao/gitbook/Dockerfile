FROM node:slim

# calibre && bzip2
RUN apt-get update && \
  apt-get install -y calibre bzip2 && \
  apt-get clean && \
  rm -rf /var/cache/apt/* /var/lib/apt/lists/*
# svgexport
RUN npm i -g svgexport --unsafe-perm
# gitbook
RUN npm i -g gitbook-cli && \
  gitbook -V
# gitbook-plugins
WORKDIR /plugins
COPY book.json /plugins
RUN gitbook install
RUN npm cache clear --force && \
  rm -rf /tmp/*

WORKDIR /docs
VOLUME /docs
EXPOSE 4000

COPY entrypoint.sh /
ENTRYPOINT [ "sh", "/entrypoint.sh" ]
CMD [ "gitbook", "--help" ]