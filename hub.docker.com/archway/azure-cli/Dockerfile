FROM microsoft/azure-cli:latest

LABEL maintainer="nokuda@archway.co.jp"

ENV KUBECTL_VERSION 1.12.0
ENV HELM_VERSION 2.11.0
ENV HELM_FILENAME helm-v${HELM_VERSION}-linux-amd64.tar.gz
ENV DOTNET_SDK_VERSION 2.1.500

# install base apps
RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        make \
        go \
        vim \
        nodejs \
        yarn \
        terraform \
        krb5-libs \
        libgcc \
        libintl \
        libstdc++ \
        tzdata \
        userspace-rcu \
    && apk -X https://dl-cdn.alpinelinux.org/alpine/edge/main add --no-cache \
       lttng-ust

# install and setup Kubernetes client
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl

RUN curl -sSL https://storage.googleapis.com/kubernetes-helm/${HELM_FILENAME} | tar xz \
    && mv linux-amd64/helm /usr/local/bin/helm \
    && rm -rf linux-amd64 \
    && helm init --client-only

ENV ASPNETCORE_URLS=http://+:80 \
    # Enable detection of running in a container
    DOTNET_RUNNING_IN_CONTAINER=true \
    # Set the invariant mode since icu_libs isn't included (see https://github.com/dotnet/announcements/issues/20)
    DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=true

RUN wget -O dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_SDK_VERSION/dotnet-sdk-$DOTNET_SDK_VERSION-linux-musl-x64.tar.gz \
    && dotnet_sha512='af061f17d88e4371fe523b895b60a0259296e2cc2bd9854a04541b87038638e0a7b7053288b45bc00a89fbb04dbdb7218a76ea9dfed8919457e758c532c15e9f' \
    && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -C /usr/share/dotnet -xzf dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm dotnet.tar.gz

