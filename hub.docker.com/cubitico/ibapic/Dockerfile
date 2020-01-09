# Use an official base image
FROM amazonlinux:2

# Install python and required tools 
RUN yum install -y \
	unzip \
	python3-3.7.0 && \
	yum clean all

# download and install IB API, current latest version = 974.01 
# the first sed command corrects an bug to allow ibapi working with python 3.7 (async is now a reserved word)
# this trick should provably be removed for future ibapi versions 
# A second sed command removes the disconnection timout in client.py 

RUN curl http://interactivebrokers.github.io/downloads/twsapi_macunix.974.01.zip --output /tmp/ibapi.zip && \
	unzip /tmp/ibapi.zip -d /tmp && \
	sed -i -- 's/async/is_async/g' /tmp/IBJts/source/pythonclient/ibapi/*.py && \
	sed -i -- 's/if time.time() - timeStart > timeOut:/if False: #time.time() - timeStart > timeOut:/g' /tmp/IBJts/source/pythonclient/ibapi/client.py && \
	pip3 install /tmp/IBJts/source/pythonclient && \
	rm -fr /tmp/*

# run python
ENTRYPOINT ["python3"]
