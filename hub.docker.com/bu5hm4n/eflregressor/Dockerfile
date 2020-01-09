FROM stefanschmidt1/ci-support-files:Archlinux

# Install dependencies from enlightenment


RUN rm -rf efl

RUN git clone --depth 1 -b v1.18.5 https://git.enlightenment.org/core/efl.git

# BUILD EFL

RUN cd efl && ./autogen.sh --prefix /usr/ && make all && make install

RUN ldconfig
RUN cd ..

