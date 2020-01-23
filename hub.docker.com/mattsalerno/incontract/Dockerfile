# The first instruction is what image we want to base our container on
# We Use an official Python runtime as a parent image
FROM python:latest

# The enviroment variable ensures that the python output is set straight
# to the terminal with out buffering it first
ENV PYTHONUNBUFFERED 1

# Install some necessary things.
RUN apt-get update
RUN apt-get install -y swig libssl-dev dpkg-dev netcat

# create root directory for our project in the container
RUN mkdir /incontract

# Set the working directory to /incontract
WORKDIR /incontract
COPY . /incontract/

# Install any needed packages specified in requirements.txt
RUN pip install -U pip
RUN pip install -Ur requirements.txt
RUN python /incontract/manage.py collectstatic --noinput

CMD ["prod_run.sh"]
