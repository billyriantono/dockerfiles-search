FROM python:3.6

MAINTAINER kevin, https://github.com/thekevinchi/joinbot

# Install Dependencies
RUN apt-get update \
 && apt-get install python3-pip python3-dev python3-setuptools git supervisor -y 


# Update Pip
RUN pip3 install --upgrade pip

# Link Python3 and Pip3 to Python and Pip
RUN if [ ! -e /usr/bin/pip ]; then ln -s /usr/bin/pip3 /usr/bin/pip ; fi \
 && if [ ! -e /usr/bin/python ]; then ln -sf /usr/bin/python3 /usr/bin/python; fi 

# Cleanup
RUN rm -r /root/.cache

# Add a Volume
WORKDIR /data
VOLUME ["/data"]

