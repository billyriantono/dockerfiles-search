FROM mcr.microsoft.com/dotnet/core/sdk:3.1
RUN apt-get update && apt-get install -y dos2unix
COPY LICENSE.txt pipe.yml pipe.sh README.md /
RUN chmod +x pipe.sh
RUN dos2unix pipe.sh
ENTRYPOINT ["/pipe.sh"]