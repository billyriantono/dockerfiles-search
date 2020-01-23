FROM uber/prototool:1.8.1

RUN \
    # Install custom packages
    apk add --no-cache \
      grpc-java \
      nodejs \
      nodejs-npm && \
    # Install TypeScript protoc plugin
    npm install --global ts-protoc-gen && \
    # Remove packages only needed as part of build process
    apk del nodejs-npm && \
    # Remove cached files
    rm -rf /var/cache/apk/*
