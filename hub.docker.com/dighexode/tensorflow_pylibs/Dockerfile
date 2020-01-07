FROM baikangwang/tensorflow_cpu:emnist
MAINTAINER dighexode <dighexode@163.com>

# referenced from <>

RUN apt-get update && \
    # Dependencies
    apt-get install -y --no-install-recommends \
    python3-tk && \
	apt-get install -f && \
    apt clean && \
    apt autoremove && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 --no-cache-dir install Pillow pandas numpy matplotlib

#
# server port
#
EXPOSE 9000

CMD ["/bin/bash"]