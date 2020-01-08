FROM aergus/latex

# Install dependencies for graphviz filter.
RUN apt-get update
RUN apt-get install -y                   \
  python-pip                             \
  python-dev                             \
  graphviz                               \
  libgraphviz-dev                        \
  pkg-config
RUN pip install pygraphviz pandocfilters

# Install dependencies for minted.
RUN apt-get install -y python-pygments

# Set UTF-8 as default system encoding.
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
