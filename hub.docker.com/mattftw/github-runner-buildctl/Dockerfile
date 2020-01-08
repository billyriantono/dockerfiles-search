FROM mcr.microsoft.com/dotnet/core/runtime:3.1.0

RUN apt-get update \
  && apt-get install -y \
    git

# Install buildctl
RUN curl \
  --location \
  --silent \
  https://github.com/moby/buildkit/releases/download/v0.6.3/buildkit-v0.6.3.linux-amd64.tar.gz | tar xz -C / bin/buildctl

# Add entrypoint
ADD entrypoint /entrypoint
RUN chmod +x /entrypoint

# Create an unprivileged user
RUN useradd \
  --create-home \
  github-runner && \
    mkdir -p /home/github-runner/runner && \
    chown github-runner:github-runner -R /home/github-runner/runner
WORKDIR /home/github-runner/runner
USER github-runner

# Download the runner
RUN curl \
  --location \
  --silent \
  https://githubassets.azureedge.net/runners/2.163.1/actions-runner-linux-x64-2.163.1.tar.gz | tar xz -C . 

# Set up placeholder envvars
ENV GITHUB_TOKEN https://github.com/PLACEHOLDER/PLACEHOLDER
ENV GITHUB_URL PLACEHOLDER

ENTRYPOINT ["/entrypoint"]