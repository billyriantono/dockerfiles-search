FROM amd64/python:3-slim

LABEL maintainer="Xabi Ezpeleta <xezpeleta@gmail.com>"

# Labels
LABEL org.label-schema.schema-version="1.3"

# Install requirements
WORKDIR /usr/src/app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

# Copy source
COPY app.py .

# Run the application
ENV FLASK_APP=app.py
CMD [ "flask", "run", "--host=0.0.0.0"]
