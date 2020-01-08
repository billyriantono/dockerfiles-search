# Use an official Python runtime as a parent image
FROM python:3

RUN apt-get update && apt-get install -y --no-install-recommends git

# Copy the current directory contents into the container at /app
ADD . /app/

# Set the working directory to /app
WORKDIR /app


# Install any needed packages specified in requirements.txt
# install and cache dependencies in /tmp directory.
# doing it this way also installs any newly added dependencies.
RUN pip3 install --upgrade pip
ADD requirements.txt /tmp/requirements.txt
RUN pip3 install --trusted-host pypi.python.org -r /tmp/requirements.txt

# create user and add to docker group
RUN adduser --disabled-password --gecos '' myuser
RUN groupadd docker
RUN usermod -aG docker myuser

# grant newly created user permissions on essential files
RUN chown -R myuser:$(id -gn myuser) ~/
RUN chown -R myuser:$(id -gn myuser) /app/

# change user to newly created user
USER myuser


# Make port 80 available to the world outside this container
EXPOSE 80
EXPOSE 443

# Define environment variable
# ENV NAME World

# Run app.py when the container launches
# CMD ["python", "app.py"]
