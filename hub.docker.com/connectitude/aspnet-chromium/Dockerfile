FROM mcr.microsoft.com/dotnet/core/aspnet:3.0
RUN apt-get update && \
	apt-get install --no-install-recommends -y chromium && \
    apt-get autoremove && \
    apt-get clean
