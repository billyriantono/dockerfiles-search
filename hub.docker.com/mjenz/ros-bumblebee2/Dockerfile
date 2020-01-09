FROM mjenz/ros-indigo-perception

# ros-indigo-pointgrey-camera-driver package is missing
# https://github.com/ros-drivers/pointgrey_camera_driver/issues/188
RUN apt-get update && \
	cd /tmp && \
	curl http://snapshots.ros.org/indigo/2019-05-10/ubuntu/pool/main/r/ros-indigo-pointgrey-camera-driver/ros-indigo-pointgrey-camera-driver_0.12.2-0trusty-20181006-075556-0800_amd64.deb --output ptgrey.deb && \
	dpkg -i ptgrey.deb; \
	apt-get install -fqy && \
	rm ptgrey.deb && \
	rm -rf /var/lib/apt/lists/*

COPY ./bumblebee2.launch /
CMD ["roslaunch", "/bumblebee2.launch"]

