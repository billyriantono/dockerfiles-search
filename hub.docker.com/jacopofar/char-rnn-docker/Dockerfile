FROM kaixhin/torch:latest
RUN luarocks install nngraph
RUN luarocks install optim
RUN luarocks install nn
RUN cd / && git clone https://github.com/karpathy/char-rnn.git
WORKDIR /char-rnn
