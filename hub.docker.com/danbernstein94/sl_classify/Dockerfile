FROM ubuntu:16.04

LABEL maintainer = "danbernstein94@gmail.com"

RUN apt-get update -y && \
    apt-get install -y python3-pip python-dev git libglib2.0-0 libsm6 libxext6 libxrender-dev

COPY ./requirements.txt /app/requirements.txt

# Set the working directory to /app
WORKDIR /app

RUN pip3 install -r requirements.txt

# Copy the current directory contents into the container at /app
COPY . /app

# Make port 80 available to the world outside this container
#EXPOSE 5015:5015

ENTRYPOINT [ "python3" ]

CMD ["classify.py", "-m"]
