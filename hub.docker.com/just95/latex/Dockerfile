FROM aergus/latex

# Install newer version of Pygments (for the minted LaTeX package).
RUN apt-get update
RUN apt-get remove -y python3-pygments
RUN apt-get install -y python3-pip
RUN pip3 install Pygments

# Install Graphviz.
RUN apt-get install -y graphviz
