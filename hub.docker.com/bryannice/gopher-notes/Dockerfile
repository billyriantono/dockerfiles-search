# -----------------------------------------------------------------------------
# Stage: BASE
# -----------------------------------------------------------------------------
FROM golang:1.13-alpine as BASE

# -----------------------------------------------------------------------------
# Stage: Final
# -----------------------------------------------------------------------------
FROM python:3.8.0-alpine as FINAL

# Environment variables
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

# Copy go dir to this image
COPY --from=BASE "/go" "/go"
COPY --from=BASE "/usr/local/go" "/usr/local/go"

# Copy entrypoint files
COPY entrypoint /entrypoint

# Required Libraries
RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
        libstdc++ \
        make \
        cmake \
        clang \
        clang-dev \
        g++ \
        linux-headers \
        git \
        pkgconfig \
        libzmq \
        zeromq-dev

# Install Jupyter Notebook and lab
RUN python3 -m pip install \
        jupyter \
        jupyterlab

# install gophernotes
RUN go get -u github.com/gopherdata/gophernotes && \
    mkdir -p ~/.local/share/jupyter/kernels/gophernotes && \
    cp $GOPATH/src/github.com/gopherdata/gophernotes/kernel/* ~/.local/share/jupyter/kernels/gophernotes

WORKDIR root
ENTRYPOINT ["/entrypoint/init.py"]