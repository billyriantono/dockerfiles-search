from debian

# for Chinese, set source.list
# RUN rm /etc/apt/sources.list
# COPY ./sources.list /etc/apt/sources.list

# install dotnet-sdk
RUN apt-get update \
    && apt-get install -y curl libunwind8 gettext apt-transport-https gpg \
    && curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg \
    && mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg \
    && sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list' \
    && apt-get update \
    && apt-get install -y dotnet-sdk-2.1.101
