# tensorflow_model_server

FROM debian:jessie-slim

# Install curl
RUN apt-get update \
	&& apt-get install curl -y

# Install tensorflow-model-server
RUN echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | tee /etc/apt/sources.list.d/tensorflow-serving.list && curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | apt-key add - \
	&& apt-get update  \
	&& apt-get install tensorflow-model-server -y \
	&& tensorflow_model_server --version

CMD ["tensorflow_model_server"]
