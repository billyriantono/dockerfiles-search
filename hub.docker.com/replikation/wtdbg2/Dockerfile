FROM replikation/debian_basic
MAINTAINER Christian Brandt <christian.jena@gmail.com>
RUN git clone https://github.com/ruanjue/wtdbg2.git
WORKDIR  /wtdbg2/
RUN make
ENV PATH /wtdbg2/:$PATH
