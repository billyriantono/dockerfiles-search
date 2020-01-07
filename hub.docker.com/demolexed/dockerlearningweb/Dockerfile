# FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
# WORKDIR /app
# EXPOSE 50094
# EXPOSE 44321

# FROM microsoft/dotnet:2.1-sdk AS build
# WORKDIR /src
# RUN ls -al
# COPY ["DockerLearning.Web.csproj", "."]
# RUN dotnet restore "DockerLearning.Web.csproj"
# COPY . .
# #WORKDIR "/src/DockerLearning.Web"
# RUN dotnet build "DockerLearning.Web.csproj" -c Release -o /app

# FROM build AS publish
# RUN dotnet publish "." -c Release -o /app

# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app .
# ENTRYPOINT ["dotnet", "DockerLearning.Web.dll"]

FROM microsoft/dotnet:2.1-sdk AS builder
WORKDIR /source

# caches restore result by copying csproj file separately
COPY *.csproj .
RUN dotnet restore

# copies the rest of your code
COPY . .
RUN dotnet publish --output /app/ --configuration Release

# Stage 2
FROM microsoft/aspnetcore
WORKDIR /app
COPY --from=builder /app .
ENTRYPOINT ["dotnet", "DockerLearning.Web.dll"]