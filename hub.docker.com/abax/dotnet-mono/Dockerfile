FROM mcr.microsoft.com/dotnet/core/sdk:2.2

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch main"  | tee /etc/apt/sources.list.d/mono-official-stable.list \
  && apt-get update \
  && apt-get install -y mono-devel \
  && rm -rf /var/lib/apt/lists/* /tmp/*

ENV FrameworkPathOverride=/usr/lib/mono/4.6.1-api/
