FROM alpine:3.9
ENV DEBIAN_FRONTEND noninteractive

# Install netcore
RUN apk add --no-cache ca-certificates krb5-libs libgcc libintl libssl1.1 \
    libstdc++ lttng-ust tzdata userspace-rcu zlib icu-libs \
    nodejs yarn bash curl git

RUN wget -q https://codecov.io/bash -O /usr/bin/codecov && chmod u+x /usr/bin/codecov

ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=false \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8

ENV DOTNET_SDK_VERSION 2.2.401

RUN wget -q -O dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-musl-x64.tar.gz \
    && dotnet_sha512='89ba545c35154d7b5d40480148aff245d624ce287be4c52711ee987167feb9688b8beac92e607885b9e66a8228981df05b41e9846b6810449e8c05e170389619' \
    && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -C /usr/share/dotnet -xzf dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm dotnet.tar.gz
ENV DOTNET_USE_POLLING_FILE_WATCHER=true \ 
    NUGET_XMLDOC_MODE=skip

RUN dotnet help
RUN dotnet tool install --global dotnet-sonarscanner --version 4.6.2
RUN export PATH="${PATH}:/root/.dotnet/tools"

# Install Java
RUN apk --no-cache add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community

RUN rm -Rf /var/cache/apk
