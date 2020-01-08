FROM circleci/android:api-29-node

# Install the dependencies
RUN sudo apt-get update
RUN sudo apt-get install openssl
RUN sudo apt-get install curl
RUN sudo apt-get install sed
RUN sudo apt-get install wget

# Copy the deploy.sh
COPY deploy.sh /home/circleci/
RUN sudo chmod +x /home/circleci/deploy.sh
