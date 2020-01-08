FROM microsoft/dotnet:1.0-sdk-projectjson
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        nodejs
ADD build.sh /tmp/build.sh
CMD /tmp/build.sh