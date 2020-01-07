# Pull base image.
FROM ubuntu

# Install base software packages
RUN apt-get -qq update && apt-get -qq install wget git-core python3.6 python3-pip
RUN wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUn apt-get -qq install apt-transport-https
RUN apt-get -qq update
RUN apt-get -qq install dotnet-sdk-2.2



# Pull base image.
#FROM microsoft/aspnetcore-build

# Install base software packages
#RUN apt-get -qq update && apt-get -qq install wget git-core python3.6 python3-pip



