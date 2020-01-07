# Use Ubuntu 18.04 LTS
FROM ubuntu:18.04

# Update
RUN apt-get -y update

# Install MySQL lib
RUN apt-get -y install libmysqlclient-dev

# Install python and pip
RUN apt-get -y install python3 python-pip build-essential

# Install MySQL for Python
RUN pip install MySQL-python

# Install jam.py
RUN pip install jam.py

# Create project directory
RUN mkdir /web
RUN cd /web; jam-project.py

# Expose the 8080 port
EXPOSE 8080/tcp

# Run jam.py
CMD ["python","/web/server.py"]
