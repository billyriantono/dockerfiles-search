# Dockerfile

# FROM directive instructing base image to build upon
FROM python:3-onbuild

# COPY gunicron startup script into known file location in container
COPY start.sh /start.sh

RUN chmod +x /start.sh

# EXPOSE port 8000 to allow communication to/from server
EXPOSE 8000

# CMD specifies the command to execute to start the server running
CMD ["/start.sh"]


