FROM docker

MAINTAINER David Soff <david@soff.nl>

#	The image expects the following env vars to be set.
#	When running on opennshift this will automatically be done when using the custom build config setting
#   OUTPUT_REGISTRY - the Docker registry URL to push this image to
#   OUTPUT_IMAGE - the name to tag the image with
#   SOURCE_URI - a URI to fetch the build context from
#   SOURCE_REF - a reference to pass to Git for which commit to use (optional)
#	DOCKER_SOCKET - the socket where Docker is running on
#	PUSH_DOCKERCFG_PATH - path to docker push config

LABEL io.k8s.display-name="Generic piped builder" \
      io.k8s.description="This is an example of a piped docker builder for use with OpenShift Origin."

RUN apk add --update git openssh && \
	mkdir /root/.ssh && \
	touch /root/.ssh/known_hosts && \
	ssh-keyscan github.com >> /root/.ssh/known_hosts && \
	ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts

ENTRYPOINT cp /root/.ssh/id_rsa.ro/ssh-privatekey /root/.ssh/id_rsa && \
	chmod 400 /root/.ssh/id_rsa && \
	git clone ${SOURCE_URI} source && cd source && git checkout ${SOURCE_REF} && \
	cd .$SOURCE_CONTEXT_DIR && \
	docker build -f Dockerfile.build -t builder . && \
	docker run builder | docker build -t ${OUTPUT_REGISTRY}/${OUTPUT_IMAGE} - && \
	cp $PUSH_DOCKERCFG_PATH/.dockercfg /root/.dockercfg && \
	docker push ${OUTPUT_REGISTRY}/${OUTPUT_IMAGE}
