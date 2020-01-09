FROM microsoft/aspnetcore-build AS builder
WORKDIR /source

COPY *.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish --output /app/ --configuration Release

FROM microsoft/aspnetcore
WORKDIR /app
COPY --from=builder /app .
EXPOSE 80
CMD ["dotnet", "/app/WebApplication.dll"]
