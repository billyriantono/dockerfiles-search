FROM replikation/debian_basic
MAINTAINER Christian Brandt <christian.jena@gmail.com>
# install conda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -b -p /conda
RUN rm -f Miniconda3-latest-Linux-x86_64.sh
ENV PATH /conda/bin:$PATH
ENV DEBIAN_FRONTEND noninteractive
RUN conda install -c conda-forge git-lfs
RUN git lfs install --force
RUN git clone https://github.com/nanoporetech/ont_tutorial_basicqc.git QCTutorial
WORKDIR QCTutorial
RUN rm -rf RawData/
RUN echo 'inputFile:   "RawData/sequencing_summary.txt"' > config.yaml
RUN echo 'basecaller:  "Guppy"' >> config.yaml
RUN echo 'flowcellId:  "unknown"' >> config.yaml
RUN echo 'tutorialText: FALSE' >> config.yaml
RUN conda env create --name BasicQC --file environment.yaml
ENV PATH /conda/envs/BasicQC/bin/:$PATH
RUN echo "source activate BasicQC" > ~/.bashrc
