FROM microsoft/dotnet:latest as builder
COPY . /app
WORKDIR /app
#COPY ./Kocsistem.BugFinder.API.sln ./NuGet.config

# Copy all the csproj files and restore to cache the layer for faster builds
# The dotnet_build.sh script does this anyway, so superfluous, but docker can
# cache the intermediate images so _much_ faster
#COPY /Application/Kocsistem.BugFinder.Application/Kocsistem.BugFinder.Application.csproj  /Application/Kocsistem.BugFinder.Application/Kocsistem.BugFinder.Application.csproj
#COPY /Application/Kocsistem.BugFinder.Application.Abstractions/Kocsistem.BugFinder.Application.Abstractions.csproj  /Application/Kocsistem.BugFinder.Application.Abstractions/Kocsistem.BugFinder.Application.Abstractions.csproj

#COPY /Domain/Kocsistem.BugFinder.Domain/Kocsistem.BugFinder.Domain.csproj /Domain/Kocsistem.BugFinder.Domain/Kocsistem.BugFinder.Domain.csproj

#COPY /Infrastructure/Kocsistem.BugFinder.Infrastructure/Kocsistem.BugFinder.Infrastructure.csproj /Infrastructure/Kocsistem.BugFinder.Infrastructure/Kocsistem.BugFinder.Infrastructure.csproj
#COPY /Infrastructure/Kocsistem.BugFinder.Persistence/Kocsistem.BugFinder.Persistence.csproj /Infrastructure/Kocsistem.BugFinder.Persistence/Kocsistem.BugFinder.Persistence.csproj

#COPY /Presentation/Kocsistem.BugFinder.WebAPI/Kocsistem.BugFinder.WebAPI.csproj /Presentation/Kocsistem.BugFinder.WebAPI/Kocsistem.BugFinder.WebAPI.csproj


#COPY /Application /Application
#COPY /Domain /Domain
#COPY /Infrastructure /Infrastructure
#COPY /Presentation /Presentation

RUN file="$(ls -1)" && echo $file
RUN file="$(ls -1 Presentation/Kocsistem.BugFinder.WebAPI/)" && echo $file
#RUN file="$(ls -1 sln)" && echo $file

#run dotnet restore "Presentation/Kocsistem.BugFinder.WebAPI/Kocsistem.BugFinder.WebAPI.csproj"
#run dotnet restore
#run dotnet build

EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
ENV ASPNETCORE_ENVIRONMENT docker

ENTRYPOINT dotnet run --project "Presentation/Kocsistem.BugFinder.WebAPI/Kocsistem.BugFinder.WebAPI.csproj" -c Release

#RUN dotnet build -c Release --no-restore

#RUN dotnet publish "Presentation/Kocsistem.BugFinder.WebAPI/Kocsistem.BugFinder.WebAPI.csproj" -c Release -o ../../dist --no-restore
#RUN file="$(ls -1)" && echo $file


#Build the app image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
ARG source
WORKDIR /app/dist
ENV ASPNETCORE_ENVIRONMENT Local
#COPY --from=builder dist .
COPY ${source:-dist} .
ENTRYPOINT ["dotnet", "Kocsistem.BugFinder.WebAPI.dll"]
