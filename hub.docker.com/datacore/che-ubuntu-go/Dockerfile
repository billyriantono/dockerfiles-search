FROM eclipse/ubuntu_jre
RUN sudo apt-get update && \
	sudo apt-get install -y --no-install-recommends \
			g++ \
			gcc \
			libc6-dev \
			make \
			&& sudo rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.7.3
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 508028aac0654e993564b6e2014bf2d4a9751e3b286661b0b0040046cf18028e

RUN sudo curl -fsSL "${GOLANG_DOWNLOAD_URL}" -o golang.tar.gz && \
	echo "${GOLANG_DOWNLOAD_SHA256} golang.tar.gz" | sha256sum -c - && \
	sudo tar -C /usr/local -xzf golang.tar.gz && \
	sudo rm golang.tar.gz

RUN sudo mkdir -p /go/bin /go/pkg /go/src && \
	sudo chmod -R 777 /go && \
	sudo mkdir -p /projects/bin /projects/pkg /projects/src && \
	sudo chmod -R 777 /projects

ENV PATH /projects/bin:/go/bin:/usr/local/go/bin:$PATH
ENV CHE_PROJECTS_ROOT=/projects/src

EXPOSE 8080

CMD tail -f /dev/null
