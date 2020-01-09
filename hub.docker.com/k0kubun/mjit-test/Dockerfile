FROM k0kubun/ruby:2.6.0-preview2

# Some timezone tests don't succeed without tzdata.
# Sudo is for running some commands as root.
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata sudo

# Some file permission tests don't succeed with root.
RUN useradd --shell /bin/bash --create-home test
