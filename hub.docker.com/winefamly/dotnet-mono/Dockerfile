FROM mcr.microsoft.com/dotnet/core/sdk:3.0.100

ENV MONO_VERSION="6.0"

RUN apt-get update
RUN apt-get install -y --no-install-recommends gnupg dirmngr

RUN export GNUPGHOME="$(mktemp -d)"
RUN gpg --batch --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
RUN gpg --batch --export --armor 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF > /etc/apt/trusted.gpg.d/mono.gpg.asc
RUN gpgconf --kill all
RUN rm -rf "$GNUPGHOME"
RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch/snapshots/$MONO_VERSION main" >> /etc/apt/sources.list.d/mono-official-stable.list
RUN apt-get update
RUN apt-get install -y mono-runtime

RUN apt-get purge -y --auto-remove gnupg dirmngr
RUN rm -rf /var/lib/apt/lists/* /tmp/*
