FROM jetbrains/teamcity-agent:2018.1.2

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Install docker-compose (the apt-get version is old--this is the suggested install method on the docker-compose github page)
# https://github.com/docker/compose/releases/tag/1.21.2
RUN curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose

# Update the list of products
RUN apt-get update && apt-get install -y build-essential

RUN apt-get install -y wget

#Install latest package for PoweShell Core
#PowerShell Core, for Linux, is published to package repositories for easy installation (and updates). This is the preferred method.
# Download the Microsoft repository GPG keys
RUN wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
RUN dpkg -i packages-microsoft-prod.deb
RUN apt-get install -f

# Update the list of products
RUN apt-get update

# Install PowerShell
RUN apt-get install -y powershell

#Install psake
#psake is a build automation tool written in PowerShell. It avoids the angle-bracket tax associated with executable 
#XML by leveraging the PowerShell syntax in your build scripts. psake has a syntax inspired by rake (aka make in Ruby) and 
#bake (aka make in Boo), but is easier to script because it leverages your existent command-line knowledge.
RUN pwsh -command "Set-PSRepository -Name PSGallery -InstallationPolicy Trusted"
RUN pwsh  -command "Install-Module -Name psake -RequiredVersion 4.7.4"

#Install Pester
#Pester is the ubiquitous test and mock framework for PowerShell.
RUN pwsh -command "Install-Module -Name Pester -Force -SkipPublisherCheck"