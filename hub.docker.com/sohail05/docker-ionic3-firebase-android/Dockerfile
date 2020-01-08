FROM sohail05/docker-ionic:latest

# Make use of -y -q in conjuction to avoid user interaction prompts
ENV DEBIAN_FRONTEND noninteractive
ENV PATH=$PATH:/opt/gradle/gradle-4.3.1/bin
# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

RUN npm install -g firebase-tools