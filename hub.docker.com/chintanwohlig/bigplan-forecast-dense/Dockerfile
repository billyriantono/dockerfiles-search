# Use an official Python runtime as a parent image
FROM python:3.6.6

# Set the working directory to /app
WORKDIR /Forecast_Engine_Dense

# Copy the current directory contents into the container at /app
ADD . /Forecast_Engine_Dense

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 8586 available to the world outside this container
EXPOSE 8586

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
