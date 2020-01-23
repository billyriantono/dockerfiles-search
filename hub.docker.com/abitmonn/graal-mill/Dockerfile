
# Pull base image
#FROM openjdk:8u181
FROM oracle/graalvm-ce:1.0.0-rc12

# Env variables
ENV SCALA_VERSION 2.12.8
ENV MILL_VERSION 0.3.5

# Define working directory
WORKDIR /root


# Install mill
RUN sh -c '(echo "#!/usr/bin/env sh" && curl -L https://github.com/lihaoyi/mill/releases/download/${MILL_VERSION}/${MILL_VERSION}) > /usr/local/bin/mill && chmod +x /usr/local/bin/mill'
