FROM python:3
ENV PYTHONUNBUFFERED 1
ENV PORT 8000

RUN useradd -ms /bin/bash django

USER django

# Set env variables used in this Dockerfile (add a unique prefix, such as DOCKYARD)
# Local directory with project source
ENV DOCKYARD_SRC=tiny
# Directory in container for all project files
ENV DOCKYARD_SRVHOME=/home/django
# Directory in container for project source files
ENV DOCKYARD_SRVPROJ=$DOCKYARD_SRVHOME/$DOCKYARD_SRC

# Create application subdirectories
WORKDIR $DOCKYARD_SRVHOME
RUN mkdir media static logs
VOLUME ["$DOCKYARD_SRVHOME/media/", "$DOCKYARD_SRVHOME/logs/"]

# Copy application source code to SRCDIR
COPY $DOCKYARD_SRC $DOCKYARD_SRVPROJ

# Install Python dependencies
RUN pip install -r $DOCKYARD_SRVPROJ/requirements/base.txt --user

# Port to expose
EXPOSE $PORT

# Copy entrypoint script into the image
WORKDIR $DOCKYARD_SRVPROJ
COPY ./docker-entrypoint.sh /
USER root
RUN chmod +x /docker-entrypoint.sh
USER django
ENTRYPOINT /docker-entrypoint.sh ${PORT}
