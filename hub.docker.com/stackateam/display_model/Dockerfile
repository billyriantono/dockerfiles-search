# Use an official Python runtime as a parent image
FROM python:3.6

# Set the working directory to /app
WORKDIR /app
RUN apt-get install curl

# Copy the current directory contents into the container at /app
COPY . /app
RUN curl https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.fr.300.bin.gz --output cc.fr.300.bin.gz
Run gunzip cc.fr.300.bin.gz

# Install from Pipfile
RUN pip install pipenv==2018.10.13
RUN pipenv install --deploy

#run the test suite
#RUN pipenv run py.test test.py

# Make port 80 available to the world outside this container
EXPOSE 8000

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["pipenv", "run", "uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]


# docker build -t stackateam/display_model . --rm
# docker run -p 80:8000 stackateam/display_model

