FROM python:3.6

# Set the build args
ONBUILD ARG PIP_INDEX_URL='https://pypi.python.org/simple'
ONBUILD ARG PIP_EXTRA_INDEX_URL
ONBUILD ARG PIP_TRUSTED_HOST

# Set environment
ENV PY_UID 1000
ENV PY_USER python
ENV PY_PRJ_DIR /usr/src/app
ENV PY_LIB_DIR /usr/local

USER root

# Install gettext for django translations
RUN apt-get update --fix-missing && \
    apt-get install -y gettext nano

# Create user 'python' with UID=1000 and in the 'users' group
RUN useradd -m -s /bin/bash -N -u $PY_UID $PY_USER

# Create and set working directory and set user 'python' as its owner
RUN mkdir -p $PY_PRJ_DIR
RUN chown -R $PY_USER $PY_PRJ_DIR
WORKDIR $PY_PRJ_DIR

# Set user 'python' as the owner of the /usr/local directory
RUN chown -R $PY_USER $PY_LIB_DIR

# Intall required python libraries
ONBUILD COPY requirements.txt $PY_PRJ_DIR
ONBUILD RUN pip install --no-cache-dir -r requirements.txt

# Copy entire project directory into container
ONBUILD COPY . $PY_PRJ_DIR

# Switch back to python to avoid container running accidentally as root
USER $PY_USER
