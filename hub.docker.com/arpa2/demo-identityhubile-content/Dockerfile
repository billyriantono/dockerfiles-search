FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM base AS final
WORKDIR /app
ENV APPNAME *
run echo "dotnet ${APPNAME}"
CMD dotnet ${APPNAME}
