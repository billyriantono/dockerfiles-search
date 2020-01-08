FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /api
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY IDE-Solution.sln ./
COPY Wealz.IDE.Core/ Wealz.IDE.Core/
COPY Wealz.IDE.Designer/ Wealz.IDE.Designer/
COPY Wealz.IDE.Mvc/ Wealz.IDE.Mvc/
COPY Wealz.IDE.Portal/ Wealz.IDE.Portal/
COPY Wealz.IDE.Resource.Ext/ Wealz.IDE.Resource.Ext/
COPY Wealz.IDE.Utility/ Wealz.IDE.Utility/
COPY Wealz.IDE.Test/ Wealz.IDE.Test/
RUN dotnet restore
#COPY . .
WORKDIR /src/Wealz.IDE.Portal
RUN dotnet build -c Release -o /Portal

FROM build AS publish
RUN dotnet publish -c Release -o /Portal

FROM base AS final
WORKDIR /Portal
COPY --from=publish /Portal .
ENTRYPOINT ["dotnet", "Wealz.IDE.Portal.dll"]
