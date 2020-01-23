# Use an official Python runtime as an image
FROM python:latest

RUN pip3 install --upgrade pip

RUN curl https://pypi.python.org

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y

RUN apt-get autoclean -y
RUN apt-get autoremove -y
RUN apt clean -y

WORKDIR /app

# Sets the working directory for following COPY and CMD instructions
# Notice we haven’t created a directory by this name - this
# instruction creates a directory with this name if it doesn’t exist
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip3 install --no-cache-dir -r requirements.txt

# Run app.py when the container launches
ENTRYPOINT ["python3"]
CMD ["app.py"]
