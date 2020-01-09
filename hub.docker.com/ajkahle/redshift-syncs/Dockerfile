# Use an official Python runtime as a parent image
FROM python:3.7

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install pandas sqlalchemy psycopg2 sqlalchemy-redshift gspread-pandas

# Run app.py when the container launches
CMD ["python", "/app/start.py"]
