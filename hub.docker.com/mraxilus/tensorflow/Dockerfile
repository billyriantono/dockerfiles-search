# Base image off of TensorFlow's latest GPU development image.
from tensorflow/tensorflow:latest-devel-gpu-py3

# Provide image details.
label maintainer "Emmanuel Smith (esmith@projectaxil.us)"


# Expose port for Jupyter notebook server.
expose 8888

# Install Keras.
run pip3 install \
      h5py \
      keras

# Configure Keras to use TensorFlow for its backend.
env KERAS_BACKEND=tensorflow

# Setup image entry point.
run mkdir /root/tensorflow
workdir /root/tensorflow

# Start command line for user.
cmd ["bash"]
