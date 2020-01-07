FROM tensorflow/tensorflow:latest-gpu-py3 AS ml2
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
	pip3 install \
		numpy \
		scipy \
		sklearn \
		keras \
		cntk-gpu \
		allennlp 
	