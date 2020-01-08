FROM microsoft/dotnet:${dotnet_core_runtime_version:-2.2-runtime}

################################################################################
##### Add services and packages for backend

RUN echo 'APT::Install-Recommends "0";' > /etc/apt/apt.conf.d/99norecommends && \
    echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/99norecommends

# packages for our backend
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -y locales locales-all unzip bzip2 curl wget libgdiplus && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set timezone and locale
RUN echo "Europe/Moscow" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata && \
    locale-gen en_US.UTF-8 && update-locale LANG=en_US.UTF-8

# Add user
RUN useradd -s /bin/bash -m transporter

RUN dotnet --info
