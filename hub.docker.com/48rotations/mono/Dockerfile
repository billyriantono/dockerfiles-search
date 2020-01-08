FROM 48rotations/mono:base

# Install debug tools
RUN apk add --no-cache \
      git \
      docker \
      jq \
      curl \
      vim

# Can't run Docker-in-Docker (dind), so no need to start
# anything. CircleCI offers a remote Docker Engine host, see
# https://circleci.com/docs/2.0/building-docker-images/.

# Download kubectl
ADD https://storage.googleapis.com/kubernetes-release/release/v1.12.2/bin/linux/amd64/kubectl /bin/kubectl
RUN chmod +x /bin/kubectl

# Copy scripts used in CI/CD
COPY ./bin/checkout /bin/checkout
COPY ./bin/build    /bin/build
COPY ./bin/deploy   /bin/deploy
