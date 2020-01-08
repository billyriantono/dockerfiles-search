FROM debian:jessie
ENV RUNTIME_PACKAGES="ruby"
ENV BUILD_PACKAGES="ruby-dev gcc libssl-dev build-essential"
RUN apt-get -y update && apt-get install -y $RUNTIME_PACKAGES $BUILD_PACKAGES
RUN gem install dotenv ably eventmachine logger json mqtt
RUN apt-get remove -y $BUILD_PACKAGES && apt-get autoremove -y
