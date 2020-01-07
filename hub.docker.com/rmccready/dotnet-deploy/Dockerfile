FROM mcr.microsoft.com/dotnet/core/sdk:3.1

#
# Setup apt-transport-https needed first to be able to download new repository info on https
#
RUN apt-get update && apt-get install -y apt-transport-https
	
#
# Install utilities needed for deployment
#
RUN apt-get update && apt-get install -y \
		lftp

#
# Setup environment so default login is in writable folder for build
#
ENV HOME /tmp
WORKDIR /tmp
