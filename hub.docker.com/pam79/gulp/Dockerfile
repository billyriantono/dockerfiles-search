FROM pam79/node:v12.14.0
LABEL maintainer="Paapa Abdullah Morgan <paapaabdullahm@gmail.com>"

RUN npm -g install gulp-cli@2.2.0; \
    npm install gulp -D; \
    npx -p touch nodetouch gulpfile.js; \
    gulp --help;

WORKDIR /src

ENTRYPOINT ["gulp"]
