# We Use an official Python runtime as a parent image
FROM python:3.7-alpine

# The enviroment variable ensures that the python output is set straight
# to the terminal with out buffering it first
ENV PYTHONUNBUFFERED 1

# create root directory for our project in the container
RUN mkdir /froney_backend

# Set the working directory to /froney_backend
WORKDIR /froney_backend

# Copy the current directory contents into the container at /froney_backend
ADD . /froney_backend/

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Expose port 80 and run the server
EXPOSE 80
STOPSIGNAL SIGINT
ENTRYPOINT ["python", "manage.py"]
CMD ["runserver", "0.0.0.0:80"]