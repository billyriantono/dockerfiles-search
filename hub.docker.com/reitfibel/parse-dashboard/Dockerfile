FROM node
MAINTAINER David Enke <post@davidenke.de>

ENTRYPOINT ["/usr/local/bin/parse-dashboard", "--allowInsecureHTTP"]
EXPOSE 4040
RUN npm install -g parse-dashboard
