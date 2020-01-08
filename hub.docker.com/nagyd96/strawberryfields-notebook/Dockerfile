FROM nagyd96/jupyter-notebook-base:latest
USER root

# Install pytorch 1.3.1 with torchvision
RUN python3 -m pip install torch==1.3.1 torchvision==0.4.2

# Install Strawberry Fields and TensorFlow with GPU and CUDA support
RUN python3 -m pip install strawberryfields tensorflow-gpu==1.3
