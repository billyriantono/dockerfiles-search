FROM weigun/bitbuilder:baseEnv

WORKDIR ${TOOLS}
 
# build mongodb
RUN curl -LO http://downloads.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && \
    tar -xzf mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && \
    rm -f mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && \
    export PATH=${PATH}:${TOOLS}/mongodb-linux-x86_64-ubuntu1804-4.1.1/bin
# build mongodb c driver
RUN curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.13.0/mongo-c-driver-1.13.0.tar.gz && \
    tar -xzf mongo-c-driver-1.13.0.tar.gz && \
    cd mongo-c-driver-1.13.0 && \
    mkdir -p ${TOOLS}/mongo-cdriver && \
    mkdir -p build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${TOOLS}/mongo-cdriver" -DENABLE_BSON=ON -DENABLE_SSL=OPENSSL -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DENABLE_STATIC=ON .. && \
    make -j$(nproc) && \
    make install && \
    export PATH=${TOOLS}/mongo-cdriver:$PATH && \
    cd ${TOOLS} && \
    rm -rf mongo-c-driver-1.13.0.tar.gz mongo-c-driver-1.13.0

# build mongodb cxx driver
RUN curl -L https://github.com/mongodb/mongo-cxx-driver/archive/r3.4.0.tar.gz -o mongo-cxx-driver-r3.4.0.tar.gz && \
    tar -xzf mongo-cxx-driver-r3.4.0.tar.gz && \
    cd mongo-cxx-driver-r3.4.0 && \
    sed -i 's/\"maxAwaitTimeMS\", count/\"maxAwaitTimeMS\", static_cast<int64_t>(count)/' src/mongocxx/options/change_stream.cpp && \
    sed -i 's/add_subdirectory(test)//' src/mongocxx/CMakeLists.txt src/bsoncxx/CMakeLists.txt && \
    mkdir -p build && \
    cd build && \
    mkdir -p ${TOOLS}/mongo-cxxdriver && \
    cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="${TOOLS}/mongo-cxxdriver" -DCMAKE_PREFIX_PATH="${TOOLS}/mongo-cdriver;${TOOLS}/mongo-cxx-driver-r3.4.0" .. && \
    make -j$(nproc) && \
    make install && \
    export PATH=${TOOLS}/mongo-cxxdriver:$PATH && \
    cd ${TOOLS} && \
    rm -rf mongo-cxx-driver-r3.4.0.tar.gz mongo-cxx-driver-r3.4.0
