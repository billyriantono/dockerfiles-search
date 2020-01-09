FROM microsoft/dotnet:2.2-sdk AS build
COPY . /src/
WORKDIR src/Fokko.ThePieces.Crawler
RUN dotnet restore && \
    dotnet publish -c Release -o /app


FROM microsoft/dotnet:2.2-runtime AS runtime
COPY --from=build /app .


ENTRYPOINT ["dotnet", "Fokko.ThePieces.Crawler.dll"]