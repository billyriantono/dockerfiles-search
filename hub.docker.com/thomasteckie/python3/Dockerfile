# our base image
FROM ubuntu

# Install python and pip
RUN apt update
RUN apt-get upgrade -y
RUN apt-get install -y nano
RUN apt-get install -y python3 python3-pip python3-dev

# install Python modules needed by the Python app
RUN pip3 install -U pip
RUN pip install -U scipy


# run the application
CMD ["python3"]
