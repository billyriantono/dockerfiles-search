# Use an official Python runtime as a parent image
FROM python:2

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
ADD requirements.txt /app/
RUN apt-get update && \
    apt-get install -y gcc \
                       xmlsec1 \
                       libffi-dev \
                       libjpeg-dev \
                       python-dev
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Define environment variable
ENV NAME djangoapp

# Set up virtual env. Deprecate this once the Docker container is solid.
RUN pip install virtualenvwrapper

RUN echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python" >> /root/.bashrc
RUN echo "export WORKON_HOME=~/.venvs" >> /root/.bashrc
RUN echo "source /usr/local/bin/virtualenvwrapper.sh" >> /root/.bashrc
RUN echo "export PIP_DOWNLOAD_CACHE=$HOME/.pip-downloads" >> /root/.bashrc
RUN cat /root/.bashrc  # check lines added

RUN ls -a /root
RUN /bin/bash -c "source $(find / -name "virtualenvwrapper.sh") && \
    mkvirtualenv BetterWorks && \
    workon BetterWorks"

