FROM alpine:edge as mbedtlsBuilder
MAINTAINER Jose Cabral <cabralcochi@gmail.com>
WORKDIR /
RUN apk add --no-cache bash git gcc g++ make cmake \
    && git clone -b mbedtls-2.7.1 https://github.com/ARMmbed/mbedtls mbedtls \
	&& cd mbedtls \
	&& mkdir build \
	&& cd build \
	&& cmake -DENABLE_TESTING=Off ../ \
	&& make -j8 

FROM alpine:edge as opcuaBuilder
WORKDIR /
COPY --from=mbedtlsBuilder /mbedtls /mbedtls
RUN  apk add --no-cache bash git cmake gcc make g++ python py-pip py-six \
	&& git clone -b v1.0 https://github.com/open62541/open62541.git open62541 \
    && cd open62541 \
	&& git submodule update --init --recursive \
	&& mkdir build/ \
	&& cd build/ \
	&& cmake -DCMAKE_BUILD_TYPE=Release \
          -DUA_ENABLE_AMALGAMATION=ON \
		  -DUA_ENABLE_ENCRYPTION=ON \
		  -DMBEDCRYPTO_LIBRARY=/mbedtls/build/crypto/library/libmbedcrypto.a \
		  -DMBEDTLS_INCLUDE_DIRS=/mbedtls/include \
		  -DMBEDTLS_LIBRARY=/mbedtls/build/library/libmbedtls.a \
		  -DMBEDX509_LIBRARY=/mbedtls/build/library/libmbedx509.a \
		  ../ \
    && make -j8 

FROM alpine:edge as forteBuilder
WORKDIR /
COPY --from=mbedtlsBuilder /mbedtls /mbedtls
COPY --from=opcuaBuilder /open62541 /open62541
RUN apk add --no-cache bash git cmake gcc make g++ \
	&& git clone -b develop https://git.eclipse.org/r/4diac/org.eclipse.4diac.forte \
    && cd org.eclipse.4diac.forte \
	&& mkdir build \ 
	&& cd build \
	&& cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release \
        -DFORTE_ARCHITECTURE=Posix \
		-DFORTE_MODULE_CONVERT=ON \
		-DFORTE_MODULE_UTILS=ON \
        -DFORTE_COM_ETH=ON \
		-DFORTE_MODULE_IEC61131=ON \
        -DFORTE_COM_OPC_UA=ON \
        -DFORTE_COM_OPC_UA_INCLUDE_DIR=/open62541/build/ \
        -DFORTE_COM_OPC_UA_LIB_DIR=/open62541/build/bin \
        -DFORTE_COM_OPC_UA_LIB=libopen62541.a \
		-DFORTE_COM_OPC_UA_MASTER_BRANCH=ON \
		-DFORTE_COM_OPC_UA_ENCRYPTION=ON \
		-DFORTE_COM_OPC_UA_ENCRYPTION_INCLUDE_DIR=/mbedtls/include \
		-DFORTE_COM_OPC_UA_ENCRYPTION_LIB_DIR="/mbedtls/build/crypto/library/;/mbedtls/build/library/" \
		../ \
    && make -j8 

FROM alpine:edge
WORKDIR /
COPY --from=forteBuilder org.eclipse.4diac.forte/build/src/forte .
RUN apk add --no-cache libstdc++

EXPOSE 4840 4841 4842 61499 61500 61501 61502 61503 61504 61505
CMD /forte
