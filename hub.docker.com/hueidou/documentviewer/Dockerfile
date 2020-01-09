FROM hueidou/converter AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["DocumentViewer.csproj", "./"]
RUN dotnet restore "DocumentViewer.csproj"
COPY . .
RUN dotnet build "DocumentViewer.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DocumentViewer.csproj" -c Release -r linux-x64 --self-contained true -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["./DocumentViewer"]