FROM	sin1/rose_compiler
RUN	cd /opt && \
	git clone https://github.com/kazuho/picojson.git && \
	mkdir /root/src && \
	cd /root/src && \
	wget http://archive.apache.org/dist/xerces/c/3/sources/xerces-c-3.1.1.tar.gz && \
	mkdir xerces && \
	tar xf xerces-c-3.1.1.tar.gz -C xerces --strip-components=1 && \
	cd /root/src/xerces && \
	./configure --prefix=/opt/xerces-c && \
	make && \
	make install && \
	cd /root/src && \
	wget http://www-eu.apache.org/dist/xalan/xalan-c/sources/xalan_c-1.11-src.tar.gz && \
	mkdir xalan && \
	tar xf xalan_c-1.11-src.tar.gz -C xalan --strip-components=1 && \
	cd /root/src/xalan/c && \
	export XERCESCROOT=/opt/xerces-c && \
	export XALANCROOT=/root/src/xalan/c && \
	./runConfigure -p linux -c gcc -x g++ -P /opt/xalan-c && \
	make && \
	make install && \
	cd /root/src && \
	wget https://cmake.org/files/v3.1/cmake-3.1.0-Linux-x86_64.tar.gz && \
	tar xf cmake-3.1.0-Linux-x86_64.tar.gz -C /usr --strip-components=1 && \
	cd /root/src && \
	git clone https://github.com/xevolver/xevxml.git && \
	source /opt/rose/setPATH.sh && \
	export CMAKE_LIBRARY_PATH=/opt/rose/lib:/opt/boost-1.54/lib:/opt/xerces-c/lib:/opt/xalan-c/lib:$CMAKE_LIBRARY_PATH && \
	export CMAKE_INCLUDE_PATH=/opt/rose/include/rose:/opt/boost-1.54/include:/opt/xerces-c/include:/opt/xalan-c/include:/opt/picojson:$CMAKE_INCLUDE_PATH && \
	cd /root/src/xevxml && \
	mkdir mybuild &&\
	cd /root/src/xevxml/mybuild && \
	cmake -DCMAKE_INSTALL_PREFIX=/opt/xevxml ../ && \
	make -j8 && \
	make install && \
	cd /root && \
	rm -rf /root/src && \
	echo 'source /opt/xevxml/bin/xevxml_vars.sh' > /etc/profile.d/xevxml.sh
