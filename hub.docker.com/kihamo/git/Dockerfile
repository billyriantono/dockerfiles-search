FROM alpine:latest

RUN apk --no-cache add \
    git \
    bash \
    openssh-client \
    rsync \
    ncurses \
    make

RUN git clone https://github.com/tj/git-extras.git \
    && cd git-extras \
    && git checkout $(git describe --tags $(git rev-list --tags --max-count=1)) &> /dev/null \
    && make install \
    && cd ../ \
    && rm -rf git-extras

ENTRYPOINT ["/bin/bash"]