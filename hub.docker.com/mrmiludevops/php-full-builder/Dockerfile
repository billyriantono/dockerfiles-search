FROM bartos/php-builder

RUN apk update && \
    apk add --no-cache \
    git \
    ruby \
    ruby-dev  \
    ruby-rdoc \
    build-base \
    libnotify \
    autoconf \
    nasm \
    automake

RUN gem install sass

RUN ln -s /usr/bin/sass /usr/local/bin/sass

RUN npm install -g \
    uglifycss \
    uglify-js \
    gulp \
    notify-send \
    gulp-notify
