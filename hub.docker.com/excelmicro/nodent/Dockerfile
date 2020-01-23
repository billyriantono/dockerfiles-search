# DockerFile for wflow
# the input data root directory should be mounted as /data
FROM ewatercycle/pcraster-container:latest
MAINTAINER Gijs van den Oord <g.vandenoord@esciencecenter.nl>
COPY . /opt/wflow/
RUN pip install netCDF4 gdal pyproj matplotlib scipy cython && pip install netcdftime
WORKDIR /opt/wflow/wflow-py
RUN python setup.py install
VOLUME /data
ENV PYTHONPATH /usr/local/python/
WORKDIR /
ENTRYPOINT ["python","/usr/local/bin/wflow_sbm.py","-C","/data"]
