# Pull base image
FROM centos:7

# Install git
RUN yum install git -y

# Install java
RUN yum install java-1.8.0-openjdk -y
RUN yum install java-1.8.0-openjdk-devel -y

# Create file
RUN mkdir folder
#RUN cat > folder/readme.txt
RUN echo 'This is readme.txt file' > folder/readme.txt

# Default command
CMD ["bash"]