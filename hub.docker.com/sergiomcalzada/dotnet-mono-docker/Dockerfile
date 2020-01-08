FROM mcr.microsoft.com/dotnet/core/sdk:3.0

RUN apt-get update -y \
    && apt-get install \
    gnupg \
    gnupg1 \
    gnupg2 \
    dirmngr \
    -y \
    --no-install-recommends \
    --no-install-suggests

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
	&& echo "deb http://download.mono-project.com/repo/debian wheezy-libjpeg62-compat main" | tee -a /etc/apt/sources.list.d/mono-xamarin.list \
	&& echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots/4.4.2.11 main" | tee -a /etc/apt/sources.list.d/mono-xamarin.list \
	&& apt-get update \
	&& apt-get install -y mono-devel ca-certificates-mono fsharp mono-vbnc nuget referenceassemblies-pcl \
	&& rm -rf /var/lib/apt/lists/*

RUN apt-get update -y \
    && apt-get install \
        -y \
        --no-install-recommends \
        --no-install-suggests \
        mono-devel \
        mono-xsp4 \
        ca-certificates-mono \
        referenceassemblies-pcl \
        nuget \
    && nuget update -Self \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get autoremove -y \
    && apt-get autoclean -y