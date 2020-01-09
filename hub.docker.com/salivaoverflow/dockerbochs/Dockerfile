FROM salivaoverflow/droidide:1.10
RUN apt-get install -y byacc nasm bochs-x && cd /root && \
	git clone https://github.com/salivaoverflow/bochs && \
	cd bochs && ./configure --enable-debugger --enable-disasm && \
	make && make install && cd /root && rm -rf bochs
