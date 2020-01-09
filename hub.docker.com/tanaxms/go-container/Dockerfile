FROM golang:1.10.3-alpine

# Mount the projects folder.
VOLUME [ "/projects" ]

# Remove our default go src folder.
RUN rmdir /go/src

WORKDIR /go

# Create symlink folder called src, pointing to our projects folder.
RUN ln -s /projects src

# Keep container running until manual shut down.
CMD cat