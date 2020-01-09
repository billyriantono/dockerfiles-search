#
# How to install oh-my-zsh in Docker image
# 
# Combine below to existing Dockerfile
#

# Base image
FROM ubuntu:16.04

# Dependencies
RUN apt-get update && \
  apt-get install -y \
  curl \
  git \
  zsh

# Install oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" || true

# Switch log-in shell to zsh
SHELL ["/bin/zsh", "-c"]

# Change oh-my-zsh theme for ROOT to "bira" from default "robbyrussell", to show host name on CUI.
RUN sed -i 's/robbyrussell/bira/' /root/.zshrc

# Base command for container
CMD ["/bin/zsh"]


