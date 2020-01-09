FROM elixir:1.8.1-alpine
LABEL maintainer "YipYip <devops@yipyip.nl>"

# SASS / inotify / node-gyp / Brunch / Webpack etc are left 
# for subsequent images to install when required.

# NPM needed for static assets build
# Bash needed for test scripts
# [make, gcc, libc-dev] needed for compiling elixir_argon2

RUN apk add --no-cache --update nodejs-npm bash make gcc libc-dev && \
    npm i npm@latest -g && \
    npm cache clean --force

CMD ["iex"]