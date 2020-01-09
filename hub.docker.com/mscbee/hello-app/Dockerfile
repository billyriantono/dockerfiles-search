# Use an official Python runtime as a parent image
FROM openjdk:8

COPY . /Users/cba50/documents/Java/Hello

# Sets the working directory 
WORKDIR /Users/cba50/documents/Java/Hello

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN javac Hello.java

# Run Hello when the container launches
CMD ["java", "Hello"]
