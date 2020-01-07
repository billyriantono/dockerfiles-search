FROM golang:latest
ENV GO111MODULE auto
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
RUN apt update && apt install -y vim pkg-config zip g++ zlib1g-dev unzip python && \
	rm -Rf /var/cache/apt/*
RUN curl -L -o bazel.sh https://github.com/bazelbuild/bazel/releases/download/$(curl -s https://api.github.com/repos/bazelbuild/bazel/releases/latest | grep tag_name | cut -d '"' -f 4)/bazel-$(curl -s https://api.github.com/repos/bazelbuild/bazel/releases/latest | grep tag_name | cut -d '"' -f 4)-installer-linux-x86_64.sh && \
	chmod +x bazel.sh && \
	./bazel.sh && \
	rm bazel.sh
RUN echo "source /usr/local/lib/bazel/bin/bazel-complete.bash" >> ~/.bashrc
