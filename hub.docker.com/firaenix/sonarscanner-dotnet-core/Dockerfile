FROM mcr.microsoft.com/dotnet/core/sdk:2.2 as base

RUN dotnet tool install --global dotnet-sonarscanner --version 4.6.0

FROM mcr.microsoft.com/dotnet/core/runtime:2.2 as runtime
COPY --from=base /root/.dotnet/tools /root/.dotnet/tools

# Make sure to add dotnet tools to the path
ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/root/.dotnet/tools"

RUN echo $PATH

# RUN dotnet-sonarscanner