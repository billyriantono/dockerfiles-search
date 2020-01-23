FROM openjdk:8-jre-alpine

# Java
RUN apk update \
    && apk upgrade \
    &&  apk --update add ca-certificates \
    &&   update-ca-certificates

RUN apk --update add ruby \
                     ruby-bigdecimal \
                     ruby-bundler \
                     ruby-irb \
                     ruby-json \
                     ruby-io-console \
                     ruby-rake \
                     ruby-rdoc \
                     libstdc++ \
                     openssl \
                     rsync \
                     tzdata \
                     wget

# Gems we need
RUN gem install asciidoctor \
                coderay


# Create the basedir
RUN mkdir -p /srv
WORKDIR /srv


# Get Swagger2Markup CLI
RUN wget https://jcenter.bintray.com/io/github/swagger2markup/swagger2markup-cli/1.3.1/swagger2markup-cli-1.3.1.jar
