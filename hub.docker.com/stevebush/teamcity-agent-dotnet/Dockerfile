# Last Updated 02/15/2019
FROM jetbrains/teamcity-agent

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
	echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list && \
	apt-get update && \
	apt-get install mono-devel -y
	
RUN apt-get install net-tools -y && \
	apt-get install iputils-ping -y

RUN curl -s -O https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893 && \
	add-apt-repository universe && \
	apt-get update && apt-get install -y --no-install-recommends apt-utils && \
	apt-get update && \
	dpkg -i packages-microsoft-prod.deb && \
	apt-get install apt-transport-https -y && \
	apt-get update && \
	apt-get install dotnet-sdk-2.2 -y
	
RUN apt-get update && \
	apt-get upgrade -y
	
	
