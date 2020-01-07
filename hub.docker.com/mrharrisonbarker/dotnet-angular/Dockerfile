FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine3.9

LABEL maintainer="mail@harrisonbarker.co.uk" \
org.label-schema.vcs-url="https://github.com/MrHarrisonBarker/dotnet-angular"

RUN apk update && apk add --update --no-cache nodejs-current nodejs-npm python make g++ openssh rsync \
&& npm install -g npm \
&& npm install -g node-sass --force --unsafe-perm=true --allow-root \
&& npm install -g @angular/cli
