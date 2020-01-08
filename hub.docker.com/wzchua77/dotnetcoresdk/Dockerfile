FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine3.9
#Install OpenJDK 8 jre for sonarscanner
RUN apk update && apk upgrade && apk add --no-cache openjdk8-jre-base

#lib for bash for ruby
RUN  apk --no-cache add ca-certificates wget bash \
&& wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
&& wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk \
&& apk add glibc-2.29-r0.apk

RUN dotnet tool install --global dotnet-sonarscanner 
ENV PATH="${PATH}:/root/.dotnet/tools"