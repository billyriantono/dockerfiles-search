# Use an official Python runtime as a parent image
FROM python:3.6

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app (necessary for requirements.txt)
ADD . /app

RUN apt-get update && \
    apt-get install -y vim

RUN pip install -r requirements.txt

RUN chmod +x jupy.sh

RUN printf 'alias jupy=/app/jupy.sh' >> ~/.bashrc

# Make port 8888 available to the world outside this container
EXPOSE 8888
