FROM gcr.io/cloudshell-images/cloudshell

# Update Step
# Cloud Shell only has some specific stuff preinstalled, but its not always up to date
RUN apt-get update && \
    apt-get -y upgrade;

# Update .NET Core
RUN apt-get remove -y dotnet-sdk-2.1 && \
    apt-get install -y dotnet-sdk-2.2;
