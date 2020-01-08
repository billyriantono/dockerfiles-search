FROM quay.io/pypa/manylinux1_x86_64

ENV GEOS_VERSION 3.5.0

# Install geos
RUN mkdir -p /src \
    && cd /src \
    && curl -f -L -O http://download.osgeo.org/geos/geos-$GEOS_VERSION.tar.bz2 \
    && tar jxf geos-$GEOS_VERSION.tar.bz2 \
    && cd /src/geos-$GEOS_VERSION \
    && ./configure \
    && make \
    && make install \
    && rm -rf /src

# Bake dev requirements into the Docker image for faster builds
ADD requirements-dev.txt /tmp/requirements-dev.txt

RUN for PYBIN in /opt/python/*/bin; do \
        $PYBIN/pip install -r /tmp/requirements-dev.txt ; \
    done

WORKDIR /io
CMD ["/io/build-linux-wheels.sh"]



# Use an official Python runtime as a parent image
FROM python:3.6-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt \
&& python setup.py install

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "HydroModelBrowser.py"]
