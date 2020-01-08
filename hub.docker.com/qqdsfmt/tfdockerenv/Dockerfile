FROM xjyu123/tf

ADD configure /
ADD python_config.sh /
COPY /configure /serving/tensorflow/configure
COPY /python_config.sh /serving/tensorflow/util/python/python_config.sh
RUN cd /serving/tensorflow && ./configure
RUN cd /serving && bazel fetch tensorflow_serving/...
RUN cd /serving && bazel fetch //tensorflow_serving/model_servers:tensorflow_model_server
 

CMD ["/bin/bash"]
