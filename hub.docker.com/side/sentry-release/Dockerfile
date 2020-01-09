FROM alpine:3.11.2

WORKDIR /

RUN apk update \
    # Update and updgrage alpine packages
    && apk upgrade \
    # Install required packages
    && apk --no-cache add bash git curl \
    # Install sentry cli
    && curl -sL https://sentry.io/get-cli/ | bash

EXPOSE 2000/udp

CMD ["bash"]
