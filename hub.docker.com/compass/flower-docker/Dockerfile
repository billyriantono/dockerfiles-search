FROM python:alpine

# Get latest root certificates
RUN apk add --update ca-certificates && update-ca-certificates

# Install the required packages
RUN pip install redis flower


# Default port
EXPOSE 5555

# Run as a non-root user by default, run as user with least privileges.
USER nobody

#ENTRYPOINT ["celery", "-A", "celery_worker.celery", "flower", "--port=5555"]
ENTRYPOINT ["flower"]
