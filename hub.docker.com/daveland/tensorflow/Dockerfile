# Set the base image
FROM gcr.io/tensorflow/tensorflow

# Dockerfile author / maintainer 
MAINTAINER Name <email.id@here> 

# Update the pip package for python 2.7 server. 
RUN pip install --upgrade \
  https://storage.googleapis.com/tensorflow/linux/cpu/protobuf-3.1.0-cp27-none-linux_x86_64.whl

# Expose default port
#EXPOSE 6379

# Set the default command
ENTRYPOINT ["/bin/bash"]
