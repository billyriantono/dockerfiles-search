FROM ruby:alpine
RUN apk add --no-cache git \
    && gem install --no-rdoc --no-ri capistrano \
    && gem install capistrano-file-permissions
WORKDIR /app
CMD ["cap"]