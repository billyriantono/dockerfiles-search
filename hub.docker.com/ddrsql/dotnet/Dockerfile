FROM microsoft/dotnet:2.2-aspnetcore-runtime
MAINTAINER ddrsql@hotmail.com

RUN apt-get update \
    && apt-get install -y --allow-unauthenticated \
        libc6-dev \
        libgdiplus \
        libx11-dev \
     && rm -rf /var/lib/apt/lists/*