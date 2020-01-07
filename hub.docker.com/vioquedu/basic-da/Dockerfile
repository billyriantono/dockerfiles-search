# Starts in Python 3.6
FROM python:3.6

# Set environment variables
ENV NB_USER=reagan \
    NB_UID=1000 \
    NB_GID=100 \
    APP_DIR=/app

# Set working directory
RUN mkdir -p $APP_DIR
WORKDIR $APP_DIR

# Copy requirements and shell script
COPY requirements.txt /app
COPY start-notebook.sh /usr/local/bin/

# Create USER
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    chown $NB_USER:$NB_GID $APP_DIR

# Install python requirements
RUN pip install -r requirements.txt

# Copy jupyter notebook configuration
COPY jupyter_notebook_config.py /etc/jupyter/

# Change to created user
USER $NB_UID