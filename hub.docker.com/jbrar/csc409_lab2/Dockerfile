# Get Java Image as a parent image
FROM openjdk:7

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD ./a1 /app

# Make port 80 available to the world outside this container
EXPOSE 8080

# Define environment variable
ENV NAME World

RUN javac URLShortner.java

# Run app.py when the container launches
CMD ["java", "URLShortner"]
