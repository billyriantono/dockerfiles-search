FROM fklab/pybuild:latest
ADD environments/docbuilder.yml /tmp/docbuilder.yml
RUN conda env create -f /tmp/docbuilder.yml

# Pull the environment name out of docbuilder.yml
RUN echo "source activate $(head -1 /tmp/docbuilder.yml | cut -d' ' -f2)" > ~/.bashrc
ENV PATH /opt/conda/envs/$(head -1 /tmp/docbuilder.yml | cut -d' ' -f2)/bin:$PATH

CMD ["/bin/bash"]
