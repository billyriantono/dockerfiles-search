FROM python:3.6	

RUN pip install numpy

RUN apt-get update \
 && apt-get install -y -q --no-install-recommends \
	zip \
	unzip \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*

RUN curl -L -o bazel-0.16.1-installer-linux-x86_64.sh https://github.com/bazelbuild/bazel/releases/download/0.16.1/bazel-0.16.1-installer-linux-x86_64.sh \
 && chmod +x bazel-0.16.1-installer-linux-x86_64.sh \
 && ./bazel-0.16.1-installer-linux-x86_64.sh --user \
 && echo export PATH="$PATH:$HOME/bin" >> /root/.bashrc 

RUN git clone --depth 1 --branch r1.10 https://github.com/tensorflow/tensorflow.git

COPY build.sh /

CMD bash -l /build.sh
