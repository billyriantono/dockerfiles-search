FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Consumers.ChannelConsumers.Telegram

RUN dotnet publish -c Release -o out Thrust.SCooB.Consumers.ChannelConsumers.Telegram.csproj


# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Consumers.ChannelConsumers.Telegram/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Consumers.ChannelConsumers.Telegram.dll"]




