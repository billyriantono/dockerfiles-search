#Build in first base / intermediate container
FROM microsoft/dotnet:2-sdk as dotnet-build
COPY TournamentManager/ /dotnet/TournamentManager

WORKDIR /dotnet/TournamentManager

RUN dotnet restore
RUN dotnet publish -c Release -o out -r linux-x64

#Run in second base
FROM microsoft/dotnet:2-runtime-jessie

#Copy build from first base to run in second base
WORKDIR /Volumes/TournamentManager
COPY --from=dotnet-build /dotnet/TournamentManager/TournamentManager/out /Volumes/TournamentManager/
COPY --from=dotnet-build /dotnet/TournamentManager/TournamentManager/appsettings.json /Volumes/TournamentManager/

ENTRYPOINT ["dotnet", "TournamentManager.dll"]
EXPOSE 5100
