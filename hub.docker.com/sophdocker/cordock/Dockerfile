FROM ubuntu

# Install Python Setuptools
RUN apt-get update \
&&  apt-get install -y python3-dev python3-pip

# Add and install Python modules
ADD cortest/requirements.txt /src/cortest/requirements.txt
RUN cd /src/cortest; pip3 install -r requirements.txt

# Bundle app source
ADD . /src
RUN mkdir -p cortest/myshare/
# Expose
EXPOSE  80

# Run
CMD ["python3", "/src/cortest/runserver.py"]
