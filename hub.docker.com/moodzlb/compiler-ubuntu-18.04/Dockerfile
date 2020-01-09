FROM ubuntu:18.04

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
  # Verify git, process tools, lsb-release (useful for CLI installs) installed
  && apt-get install --no-install-recommends -y sudo git zsh iproute2 \
  procps lsb-release build-essential ninja-build cmake cppcheck valgrind \
  # Clean up
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Create VSCode mound for extension. We don't want to re-download and re-install
RUN mkdir -p /home/$USERNAME/.vscode-server/extensions \
  /home/$USERNAME/.vscode-server-insiders/extensions \
  && chown -R $USERNAME \
  /home/$USERNAME/.vscode-server \
  /home/$USERNAME/.vscode-server-insiders

# Persist bash and zsh history
RUN SNIPPET="export HISTFILE=/commandhistory/.zsh_history" \
  && mkdir /commandhistory \
  && touch /commandhistory/.zsh_history \
  && chown -R $USERNAME /commandhistory \
  && echo $SNIPPET >> "/home/$USERNAME/.zshrc" \
  && SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
  && echo $SNIPPET >> "/root/.bashrc" \
  && touch /commandhistory/.bash_history \
  && chown -R $USERNAME /commandhistory \
  && echo $SNIPPET >> "/home/$USERNAME/.bashrc"

USER ${USERNAME}
# Install oh-my-zsh
RUN cd ~ \
  && sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" \
  && sudo ln -s .zshrc /root/.zshrc \
  && sudo ln -s .oh-my-zsh /root/.oh-my-zsh

ENTRYPOINT ["/bin/zsh"]