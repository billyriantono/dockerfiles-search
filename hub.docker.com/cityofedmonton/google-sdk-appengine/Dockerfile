# This Dockerfile is for creating cityofedmonton/google-sdk-appengine
FROM ubuntu AS legacy-appengine-sdk
WORKDIR /sdk
RUN apt-get update
RUN apt-get install wget -y
RUN apt-get install unzip -y
RUN wget https://storage.googleapis.com/appengine-sdks/featured/appengine-java-sdk-1.9.71.zip
RUN unzip appengine-java-sdk-1.9.71.zip

FROM google/cloud-sdk
COPY --from=legacy-appengine-sdk /sdk/appengine-java-sdk-1.9.71 /appengine-java-sdk

# install latest nodejs and jq for additional tools 
RUN apt-get update && curl -sL https://deb.nodesource.com/setup_11.x | bash && apt-get install nodejs jq -y