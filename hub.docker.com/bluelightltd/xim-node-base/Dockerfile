FROM bluelightltd/gt-coind-compile

COPY /  .

RUN ./autogen.sh && ./configure --with-gui=no --disable-gui-tests --disable-bench --disable-tests && make

