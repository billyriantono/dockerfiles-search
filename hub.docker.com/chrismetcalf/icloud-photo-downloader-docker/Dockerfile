FROM gliderlabs/alpine:latest
RUN apk add --update bash nodejs && rm -rf /var/cache/apk/*
RUN npm install -g grunt-cli
# Set instructions on build.
ONBUILD ADD package.json /app/
ONBUILD RUN npm install
ONBUILD ADD . /app
ONBUILD RUN grunt build

#COPY docker-entrypoint.sh /
#ENTRYPOINT ["/docker-entrypoint.sh"]

# Define working directory.
WORKDIR /app
