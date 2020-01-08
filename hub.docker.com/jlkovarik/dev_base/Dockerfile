from ubuntu:16.04
RUN apt-get update && apt-get install -y apt-utils software-properties-common && apt-add-repository ppa:ubuntu-elisp/ppa -y
RUN apt-get update && apt-get install -y emacs-snapshot git curl wget vim sudo bzip2 build-essential gnupg2 gnupg-agent
RUN useradd -c 'Default dev user' -m -d /home/dev -s /bin/bash dev
# Add symlink to pinentry for envs that have their local env configured to utilize pinentry 
RUN ln -s /usr/bin/pinentry /usr/local/bin/pinentry
RUN ln -s /usr/bin/gpg2 /usr/local/bin/gpg2
USER dev
ENV HOME /home/dev
