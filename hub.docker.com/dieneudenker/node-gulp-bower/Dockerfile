FROM node:6.17.0-jessie

# Install nasm, because it is needed for some node libraries
RUN apt-get update
RUN apt-get install nasm

# Install bower and gulp
RUN npm install -g bower@1.8.2 gulp@3.9.1

# Add possibility to have only one ssh agent running, to be
# able to save ssh key passwords to use in multiple sessions
RUN mkdir /synced_ssh_agent
COPY run_ssh_agent.sh /synced_ssh_agent/

# Define working directory.
WORKDIR /app