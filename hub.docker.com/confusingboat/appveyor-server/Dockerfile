FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim
ARG VERSION=7.0.2329

ADD https://appveyordownloads.blob.core.windows.net/appveyor/${VERSION}/appveyor-server_${VERSION}_amd64.deb /tmp/appveyor-server.deb
RUN apt update && \
  apt install /tmp/appveyor-server.deb -y && \
  rm /tmp/appveyor-server.deb

WORKDIR /opt/appveyor/server/
ENTRYPOINT ["dotnet","appveyor-server.dll"]
