FROM python:3.6-slim as package_step

RUN apt-get update && apt-get install -y --no-install-recommends \
    libsm6 libxext6 libxrender-dev libglib2.0-0

WORKDIR /opt/mobilysa
COPY camera/ camera
RUN pip install -r camera/requirements.txt
COPY camera/src/camera_gateway/conf/camera_pb2.py /usr/local/lib/python3.6/site-packages/is_msgs/

WORKDIR /opt/mobilysa/camera/src
