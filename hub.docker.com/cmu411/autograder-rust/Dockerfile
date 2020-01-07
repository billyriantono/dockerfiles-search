FROM cmu411/autograder:latest

#-----------
# RUST INSTALLATION
#-----------
# Install the latest stable version of rust. To change to a different version,
# change the word "stable" to something different (like "nightly").
# \$PATH will evaluate to the string $PATH, which is what we want.
ENV rust_version=nightly
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain $rust_version && \
  echo "export PATH=\$HOME/.cargo/bin:\$PATH" >> "$HOME/.bashrc"

################
# RUST PACKAGE INSTALLATION
################
# Install rustfmt-nightly, because it happens to have a lot of common dependencies.
# You can change this to install more things if so requested by the students.
# You might be confused why we run in a bash subshell.
#   This is because we need to source the line in the ~/.bashrc added in the
#   rust installation step. We use the RUN [...] syntax to avoid being run in sh
#   (sh -c "bash -cl ..."), which does not correctly update the environment.
RUN ["bash", "-cl", "cargo install --force rustfmt-nightly"]

#--------------
# MISC PACKAGE INSTALLATION -- common to all Dockerfiles
# Add convenience packages for students using container.
#--------------
RUN apt-get update && apt-get install -y \
  emacs \
  gdb \
  python3 \
  vim \
  ;
