FROM mcr.microsoft.com/dotnet/core/sdk:3.0
COPY LICENSE.txt pipe.yml pipe.sh README.md /
COPY Installation /usr/share/Installation
RUN apt-get update
ENTRYPOINT ["/pipe.sh"]