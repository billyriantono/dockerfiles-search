FROM ubuntu:16.04

LABEL maintainer=pierregordon@protonmail.com

# Install dependencies
RUN echo "deb http://security.ubuntu.com/ubuntu trusty-security main" >> etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        locales \
        ca-certificates \
        apt-transport-https \
        libc6 \
        libcurl3 \
        libgcc1 \
        libgssapi-krb5-2 \
        liblldb-3.6 \
        libicu52 \
        liblttng-ust0 \
        libssl1.0.0 \
        libstdc++6 \
        libunwind8 \
        libuuid1 \
        zlib1g && \
    rm -rf /var/lib/apt/lists/*

# Install .NET Core
ENV DOTNET_VERSION 1.1.2
ENV DOTNET_DOWNLOAD_URL https://dotnetcli.blob.core.windows.net/dotnet/release/1.1.0/Binaries/$DOTNET_VERSION/dotnet-debian-x64.$DOTNET_VERSION.tar.gz

RUN curl -SL $DOTNET_DOWNLOAD_URL --output dotnet.tar.gz && \
    mkdir -p /usr/share/dotnet && \
    tar -zxf dotnet.tar.gz -C /usr/share/dotnet && \
    rm dotnet.tar.gz && \
    ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

# Setup ASP.NET Core
ENV ASPNETCORE_URLS http://+:80
ENV DOTNET_HOSTING_OPTIMIZATION_CACHE /packagescache

RUN for version in '1.1.2' '1.1.3'; do \
        curl -o /tmp/aspnetcore.cache.$version.tar.gz \
            https://dist.asp.net/packagecache/$version/debian.8-x64/aspnetcore.cache.tar.gz && \
        mkdir -p /packagescache && cd /packagescache && \
        tar xvf /tmp/aspnetcore.cache.$version.tar.gz && \
        rm /tmp/aspnetcore.cache.$version.tar.gz; \
    done

# Install MSSQL tools
ENV DEBIAN_FRONTEND=noninteractive
ENV ACCEPT_EULA=Y

RUN locale-gen en_US.UTF-8 && \
    update-locale && \
    apt-get update && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | tee /etc/apt/sources.list.d/msprod.list && \
    apt-get update && \
    apt-get install -y mssql-tools && \
    rm -rf /var/lib/apt/lists/* && \
    ln -sfn /opt/mssql-tools/bin/sqlcmd /usr/bin/sqlcmd && \
    ln -sfn /opt/mssql-tools/bin/bcp /usr/bin/bcp
