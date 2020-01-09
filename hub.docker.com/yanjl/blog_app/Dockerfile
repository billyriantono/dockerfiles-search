FROM crystallang/crystal:0.24.1
LABEL  author="yanjl"

WORKDIR /home/blog
ADD . /home/blog
RUN shards build blog

WORKDIR /opt/blog/bin

RUN  mv /home/blog/bin/blog ./
ENV PATH /opt/blog/bin:$PATH

WORKDIR /home/blog
RUN rm -rf

CMD ["/bin/bash"]
