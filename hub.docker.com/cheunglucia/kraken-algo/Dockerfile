FROM tensorflow/tensorflow:latest-py3

# Install dependencies
RUN [ "pip", "install", "Flask" ]
RUN [ "pip", "install", "gunicorn" ]

# Copy files
WORKDIR /app
COPY *.py ./
COPY ./models ./models

# Define entrypoint
ENV PORT=80
EXPOSE ${PORT}
CMD gunicorn --bind 0.0.0.0:$PORT service:app