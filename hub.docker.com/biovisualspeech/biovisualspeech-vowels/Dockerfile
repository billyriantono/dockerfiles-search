FROM python:3.7-slim

WORKDIR /app

COPY . /app

FROM tiangolo/meinheld-gunicorn-flask:python3.7

COPY ./app /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 5001

# Define environment variable
ENV VARIABLE_NAME app

ENTRYPOINT ["python"]

CMD ["main.py"]