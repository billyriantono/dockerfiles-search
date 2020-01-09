FROM node:10-alpine

RUN apk --no-cache update \
&& apk --no-cache add yarn \
&& wget https://github.com/progrium/entrykit/releases/download/v0.4.0/entrykit_0.4.0_linux_x86_64.tgz \
&& tar -xvzf entrykit_0.4.0_linux_x86_64.tgz \
&& rm entrykit_0.4.0_linux_x86_64.tgz \
&& mv entrykit /usr/local/bin/ \
&& entrykit --symlink

WORKDIR /var/www/html

CMD [ "prehook", "yarn install", "--", "yarn", "watch" ]
