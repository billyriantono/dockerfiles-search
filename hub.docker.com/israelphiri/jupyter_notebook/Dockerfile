# Use the latest ubuntu image as base for the new image
# ubuntu is the base image used
FROM ubuntu:latest

# Run a system updates
# Then install python3 and pip3
RUN apt-get update && apt-get install -y python3 \
    python3-pip

# Install jupyter
RUN pip3 install jupyter

# Create a new system user
RUN useradd -ms /bin/bash jupyter

# Change to this new user
USER jupyter

# Set the container working directory to the user home folder
WORKDIR /home/jupyter

# Start the jupyter notebook using the "--ip=*" parameter to allow incoming traffic to jupyter from any IP
ENTRYPOINT ["jupyter", "notebook", "--ip=*"]
