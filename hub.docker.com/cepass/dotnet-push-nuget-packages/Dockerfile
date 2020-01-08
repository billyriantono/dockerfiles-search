FROM mcr.microsoft.com/dotnet/core/sdk:3.0
COPY LICENSE.txt pipe.yml pipe.sh README.md /
RUN chmod +x pipe.sh
ENTRYPOINT ["/pipe.sh"]