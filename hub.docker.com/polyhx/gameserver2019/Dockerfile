#Build in first base / intermediate container
FROM microsoft/dotnet:2-sdk as dotnet-build
COPY GameServer/ /dotnet/GameServer

WORKDIR /dotnet/GameServer

RUN dotnet restore
RUN dotnet publish -c Release -o out -r linux-x64

#Run in second base
FROM microsoft/dotnet:2-runtime-jessie

#Copy build from first base to run in second base
WORKDIR /Volumes/GameServer
COPY --from=dotnet-build /dotnet/GameServer/GameServer/out /Volumes/GameServer/
COPY --from=dotnet-build /dotnet/GameServer/GameServer/game.conf /Volumes/GameServer/

ENTRYPOINT ["dotnet", "GameServer.dll"]
EXPOSE 5000-5010