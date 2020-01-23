FROM selenium/standalone-chrome

# Install OpenJDK and Maven
RUN sudo apt-get update && \
    sudo apt-get install -y --no-install-recommends \
        curl \
        openjdk-8-jdk-headless \
        maven && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists

# Verify that everything works
COPY test/ test/
USER root
RUN bash ./test/run-test.sh
