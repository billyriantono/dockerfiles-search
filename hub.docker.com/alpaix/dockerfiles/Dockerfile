FROM mono:latest

MAINTAINER Alex Panov "alpaix@outlook.com"

# Update aptitude with new repo
RUN apt-get update

# Install git and dependencies
RUN apt-get install git libunwind8 gettext libicu52 -y

# clone NuGet.Client repo
RUN git clone https://github.com/NuGet/NuGet.Client.git /home/alpaix/NuGet.Client

WORKDIR /home/alpaix/NuGet.Client

CMD [ "./build.sh" ]