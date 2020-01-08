FROM microsoft/dotnet:1.0.1-sdk-projectjson
MAINTAINER "Subodh Hatkar" <subodh.hatkar@accenture.com>

# Install node
RUN bash -c "curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
             apt-get update && \
             apt-get install -y nodejs build-essential unzip && \
             npm install -g grunt"

EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
