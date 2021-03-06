FROM jetbrains/teamcity-minimal-agent:latest

MAINTAINER Vladislav Rassokhin <vladislav.rassokhin@jetbrains.com>

LABEL dockerImage.teamcity.version="latest" \
      dockerImage.teamcity.buildNumber="latest"

ENV NUGET_XMLDOC_MODE=skip \
    DOTNET_CLI_TELEMETRY_OPTOUT=true \
    DOTNET_SKIP_FIRST_TIME_EXPERIENCE=true \
    GIT_SSH_VARIANT=ssh

RUN apt-get update && \
    apt-get install -y software-properties-common apt-transport-https && \
    add-apt-repository -y ppa:openjdk-r/ppa && add-apt-repository -y ppa:git-core/ppa && apt-get update && \
    apt-get install -y git mercurial openjdk-8-jdk apt-transport-https ca-certificates && \
    \
    apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 9DC858229FC7DD38854AE2D88D81803C0EBFCD88 && \
    echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" > /etc/apt/sources.list.d/docker.list && \
    \
    apt-cache policy docker-ce && \
    apt-get update && \
    apt-get install -y docker-ce=18.03.0~ce-0~ubuntu && \
    systemctl disable docker && \
    curl -SL https://github.com/docker/compose/releases/download/1.20.1/docker-compose-Linux-x86_64 -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose && \
    \
    apt-get install -y --no-install-recommends \
            libc6 \
            libcurl3 \
            libgcc1 \
            libgssapi-krb5-2 \
            libicu55 \
            liblttng-ust0 \
            libssl1.0.0 \
            libstdc++6 \
            libunwind8 \
            libuuid1 \
            zlib1g \
        && rm -rf /var/lib/apt/lists/* && \
    \
    curl -SL https://dotnetcli.blob.core.windows.net/dotnet/Sdk/2.1.300/dotnet-sdk-2.1.300-linux-x64.tar.gz --output dotnet.tar.gz \
        && mkdir -p /usr/share/dotnet \
        && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
        && rm dotnet.tar.gz \
        && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet && \
    \
    mkdir warmup \
        && cd warmup \
        && dotnet new \
        && cd .. \
        && rm -rf warmup \
        && rm -rf /tmp/NuGetScratch && \
    \
    apt-get clean all && \
    \
    usermod -aG docker buildagent && \
    \
    add-apt-repository -y ppa:george-edison55/cmake-3.x && \
    apt-get -y install build-essential cmake --no-install-recommends && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get install -y gcc-8 g++-8 nodejs --no-install-recommends && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 800 --slave /usr/bin/g++ g++ /usr/bin/g++-8 && \
    apt-get clean all
    

# A better fix for TW-52939 Dockerfile build fails because of aufs
VOLUME /var/lib/docker

COPY run-docker.sh /services/run-docker.sh
