FROM selenium/standalone-chrome-debug:3.8.1-bohrium

USER root

#=====
# .NET Core
#=====
# Install apt-transport-https
RUN apt-get update -qqy \
  && apt-get -qqy install apt-transport-https \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# Register the trusted Microsoft signature key
ADD https://packages.microsoft.com/keys/microsoft.asc /tmp/
RUN gpg --dearmor < /tmp/microsoft.asc > /etc/apt/trusted.gpg.d/microsoft.gpg \
  && rm -f /tmp/microsoft.asc

# Register the Microsoft Product feed
RUN echo 'deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod xenial main' > /etc/apt/sources.list.d/dotnetdev.list

# Install .NET SDK
RUN apt-get update -qqy \
  && apt-get -qqy install dotnet-sdk-2.0.3 \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

USER seluser
