FROM alpine:3.2  
RUN apk update && apk --update add ruby ruby-irb ruby-io-console libstdc++ 
ADD Gemfile /app/  
RUN apk --update add --virtual build-dependencies build-base ruby-dev \  
    libc-dev linux-headers && \
    gem install bundler && \
    cd /app ; bundle install --without development test && \
    apk del build-dependencies

ADD . /app  
RUN chown -R nobody:nogroup /app  
USER nobody
WORKDIR /app
ENTRYPOINT ["./dobcast"]

