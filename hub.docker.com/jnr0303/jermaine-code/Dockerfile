from microsoft/dotnet as build
workdir /docker
run dotnet new mvc --name HelloMVC
workdir /docker/HelloMVC
run dotnet build
run dotnet publish
entrypoint [ "dotnet" ]

from microsoft/aspnetcore
workdir /publish
copy --from=build /docker/HelloMVC/bin/Debug/netcoreapp2.0/publish .
Expose 80
cmd ["dotnet", "HelloMVC.dll"]