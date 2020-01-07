# Author: Joris Penders
# Description: Image can be used as a base image for deployment of a SKLEARN-model through a Flask web API
FROM ubuntu

# Update apt-get and install required packages
RUN apt-get update && apt-get install -y python python-dev python-pip python-virtualenv

# Upgrade to the latest version of pip
RUN pip install --upgrade pip

# Install the whole scikit-learn suite
RUN pip install -U scikit-learn

# Install Flask to enable a Web API 
RUN pip install flask

# Default, start bash-prompt if interactive mode
CMD ["/bin/bash"]