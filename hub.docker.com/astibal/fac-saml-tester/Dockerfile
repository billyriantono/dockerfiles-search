# Use an official Python runtime as a parent image
FROM ubuntu:18.04

# Set the working directory to /app
WORKDIR /app

COPY getdemo.sh /app
# Copy the current directory contents into the container at /app
COPY oztemplates/ /app/oztemplates/
COPY oz.py /app
COPY run.sh /app

RUN apt-get update && apt-get install -y \
wget \
unzip 

RUN ./getdemo.sh && cp requirements.txt /tmp/


RUN apt-get update && apt-get install -y \
python-pip \
libxml2-dev \
libxmlsec1-dev \
python-dev


# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org python-saml
RUN pip install --trusted-host pypi.python.org -r /tmp/requirements.txt

# Define environment variable

# Run app.py when the container launches
CMD ["/bin/sh", "-c", "./run.sh"]

