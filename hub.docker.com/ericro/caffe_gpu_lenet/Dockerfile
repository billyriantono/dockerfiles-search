from bvlc/caffe:gpu
MAINTAINER eric <er@iex.ec>

WORKDIR $CAFFE_ROOT

RUN ./data/mnist/get_mnist.sh
RUN ./examples/mnist/create_mnist.sh
CMD ./examples/mnist/train_lenet.sh --gpu=$LGPU
