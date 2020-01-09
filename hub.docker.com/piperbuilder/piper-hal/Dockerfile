FROM piperbuilder/piper-hal-deps

RUN [ "cross-build-start" ]

# Build hook args
ARG SOURCE_COMMIT
ARG SOURCE_BRANCH

# Setup dependencies for deployment
RUN install_packages awscli debhelper dh-make

# Copy all Rust files back in
WORKDIR /home/piper/piper-hal
COPY . ./

# Compile full Rust codebase
RUN /bin/bash -c "source $HOME/.cargo/env && cargo build --release"

# Generate version hash
RUN echo "$SOURCE_COMMIT" > version.hash

RUN [ "cross-build-end" ]

CMD [ "bash" ]
