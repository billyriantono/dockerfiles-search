FROM belkakari/pytorch-basic

RUN apt-get update && apt-get install -y --no-install-recommends \
    sox \
    libsox-dev \
    libsox-fmt-all &&\
    rm -rf /var/lib/apt/lists/*

RUN conda install -y -c conda-forge librosa sox && \
    pip install kaldi_io mido pretty_midi pyo && \
    pip install torchaudio -f https://download.pytorch.org/whl/torch_stable.html
