# Multi-step Docker build for this application
#
# Usage:
# Build locally 
#   cd [project]
#   docker build -t vinlab/code-inventory-backend:latest .
# Run the app:
#   docker-compose -f src/main/docker/app.yml up -d #run docker app
#
# Suitable for Docker Hub automated builds. 
# Setup: 
#   Specify this Dockerfile in Docker Hub build settings:
#   Dockerfile location: Dockerfile.
# Pull resulting docker image to local:
#   docker login
#   docker pull vinlab/code-inventory-backend  
# Run the app:
#   docker-compose -f src/main/docker/app.yml up -d #run docker app
#
# Documentation: https://docs.docker.com/v17.09/engine/userguide/eng-image/multistage-build/
#
# Author: Andrey Potekhin

# Step 1. Build application with Maven, resulting in app.war
FROM jhipster/jhipster:v5.8.2 AS BUILD-APP-FROM-SOURCE
USER root
ADD . /code/
RUN rm -Rf /code/target /code/build /code/node_modules && \
    cd /code/ && \
    ./mvnw clean package -Pprod && \
    mv /code/target/*.war /app.war

# Step 2. Build app Docker image using app.war from previous step  
FROM vinlab/vc-inlab-cit-backend-base-image AS BUILD-APP-DOCKER-IMAGE
ENV SPRING_OUTPUT_ANSI_ENABLED=ALWAYS \
    JHIPSTER_SLEEP=0 \
    JAVA_OPTS=""
EXPOSE 10101
CMD echo "The application will start in ${JHIPSTER_SLEEP}s..." && \
    sleep ${JHIPSTER_SLEEP} && \
    java ${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom -jar /app.war "$@"
COPY --from=0 /app.war .
