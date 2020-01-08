FROM openjdk:8

# Build Tools URL
ARG BUILD_TOOLS_URL=https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar

# Version Vairable
ARG VERSION=1.13.2

# Update Image
RUN apt update && apt upgrade -y

# Create Directories
RUN mkdir /buildtools /app /data /data/worlds /data/plugins /data/conf

WORKDIR /buildtools

# Download Build Tools
RUN wget $BUILD_TOOLS_URL

# Run Build Tools
RUN java -jar BuildTools.jar --rev $VERSION

# Copy Spigot
RUN cp spigot-$VERSION.jar /app/spigot.jar

# Cleanup
RUN rm -rf /buildtools

# ADD entrypoint.sh
ADD entrypoint.sh /app/entrypoint.sh
RUN chmod +x /app/entrypoint.sh

WORKDIR /app

CMD ["entrypoint.sh"]
