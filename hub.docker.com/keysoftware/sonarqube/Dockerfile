# Debian: SonarQube 5.1 + Maven

# Pull the base image.
FROM sonarqube:5.1

# Install Maven.
RUN apt-get update && apt-get install -y maven; \
	apt-get clean; \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
