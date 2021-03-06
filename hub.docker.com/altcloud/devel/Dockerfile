FROM altcloud/base:p9

MAINTAINER alt-cloud

# install editor
RUN apt-get update && \
    apt-get install -y vim-console; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install debugging tools
RUN apt-get update && \
    apt-get install -y strace gdb; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install document viewers
RUN apt-get update && \
    apt-get install -y man; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install version control system
RUN apt-get update && \
    apt-get install -y git-core perl-Git; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install network utils
RUN apt-get update && \
    apt-get install -y curl iproute2; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install file utils
RUN apt-get update && \
    apt-get install -y lsof silver-searcher; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install shell and completions
RUN apt-get update && \
    apt-get install -y zsh zsh-completions; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

# install compilation utils
RUN apt-get update && \
    apt-get install -y make gcc gcc-c++; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

CMD ["zsh"]
