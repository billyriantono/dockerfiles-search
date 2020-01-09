FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["BlackPositivitySubmissionSite/BlackPositivitySubmissionSite.csproj", "BlackPositivitySubmissionSite/"]
COPY ["BlackPositivity.Services/BlackPositivity.Services.csproj", "BlackPositivity.Services/"]
RUN dotnet restore "BlackPositivitySubmissionSite/BlackPositivitySubmissionSite.csproj"
COPY . .
WORKDIR "/src/BlackPositivitySubmissionSite"
RUN dotnet build "BlackPositivitySubmissionSite.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BlackPositivitySubmissionSite.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BlackPositivitySubmissionSite.dll"]