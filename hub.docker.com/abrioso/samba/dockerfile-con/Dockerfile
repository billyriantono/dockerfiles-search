# Use an official Python runtime as a parent image
FROM python:3.6-slim-stretch

# Set the working directory to /app
WORKDIR /app/Source

# Copy the current directory contents into the container at /app
ADD Source /app/Source
# ADD Tables /app/Tables
ADD . /app

#Install mysqlclient
RUN apt-get update -y
RUN apt-get install -y default-libmysqlclient-dev
RUN apt-get install -y build-essential

#Install python requirements
COPY requirements.txt /app/Source
RUN pip install -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 443

# Run app.py when the container launches
CMD ["gunicorn" , "--certfile=cert.pem", "--keyfile=key.pem","-b", "0.0.0.0:443", "main:app"]
#CMD ["gunicorn", "--certfile=cert.pem --keyfile=key.pem -b 0.0.0.0:443 main:app"]


