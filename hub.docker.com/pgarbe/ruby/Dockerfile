FROM alpine:latest
MAINTAINER Philipp Garbe <philipp.garbe@web.de>

# alias rake='docker run -it --rm -v $(pwd):/root/rake \
#                        -e AWS_REGION=$AWS_REGION \
#                        -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID \
#                        -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY \
#                        -e AWS_SESSION_TOKEN=$AWS_SESSION_TOKEN \
#                        --log-driver none \
#                        --entrypoint rake OR bundle OR ruby
#                        pgarbe/rake "$@"'

ENV BUILD_PACKAGES bash curl-dev ruby-dev build-base
ENV RUBY_PACKAGES ruby ruby-io-console ruby-bundler ruby-rake

# Update and install all of the required packages.
# At the end, remove the apk cache
RUN apk update && \
    apk upgrade && \
    apk add $BUILD_PACKAGES && \
    apk add $RUBY_PACKAGES && \
    rm -rf /var/cache/apk/*

ENV HOME /root
WORKDIR $HOME/rake

ENTRYPOINT [ "ruby" ]
