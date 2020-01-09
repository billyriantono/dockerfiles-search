# TODO: Remove sources after build (in same layer)
ARG TZ='Europe/London'
FROM ubuntu as Base
ENV BUILD_ROOT='/opt/sources'
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR ${BUILD_ROOT}

# Install base requirements
RUN apt-get update && \
    echo ${TZ} > /etc/timezone && \
    apt-get install -y \
        software-properties-common \
        build-essential g++ git cmake unzip wget apt-utils \
        ffmpeg \
        libavcodec-dev \
        libavformat-dev \
        libavutil-dev \
        libeigen3-dev \
        libswscale-dev \
        libtbb-dev \
        libxerces-c-dev \
        # PDAL
        libssl-dev \
        python3-dev \
        # CGAL
        libcgal-dev \
        # qPhotoscan
        zip \
        zlib1g-dev \
        # OpenGL
        libglu1-mesa-dev \
        freeglut3-dev \
        mesa-common-dev \
        mesa-utils \
        # CC
        libpng-dev \
        libusb-dev \
        libpcap-dev \
    && \
# GDAL
# Add the UbuntuGIS PPA https://launchpad.net/~ubuntugis/+archive/ubuntu/ppa
# (can also use to install QGIS later)
    add-apt-repository --yes ppa:ubuntugis/ppa && \
    apt-get update && \
    apt-get install -y libproj-dev libgdal-dev && \
    apt-get upgrade -y && \
    apt-get install -y gdal-bin python-gdal python3-gdal libgeotiff-dev libjsoncpp-dev python-numpy \
    && \
# LASZIP
# https://github.com/LASzip/LASzip.git
    mkdir -p /tmp/LASzip && \
    cd /tmp/LASzip && \
    git init && \
    git remote add origin https://github.com/LASzip/LASzip.git && \
    git fetch --tags && \
    latestTag=$(git describe --tags `git rev-list --tags --max-count=1`) && \
    cd ${BUILD_ROOT} && rm -rf /tmp/LASzip && \
    git clone --branch $latestTag --depth 1 https://github.com/LASzip/LASzip.git LASzip \
    && \
    mkdir -p LASzip/build && \
    cd LASzip/build && \
    cmake -G "Unix Makefiles" -H${BUILD_ROOT}/LASzip -B${BUILD_ROOT}/LASzip/build \
    && make && \
    make install \
    && \
# EIGEN
    wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/eigen3/3.3.4-2/eigen3_3.3.4.orig.tar.bz2 && \
    tar xvjf eigen* && \
    cd eigen-eigen* && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release \
    .. && \
    make && \
    make install \
    && \
# FBX
# https://github.com/CloudCompare/CloudCompare/blob/master/BUILD.md#optional-setup-for-fbx-sdk-support
# https://www.autodesk.com/developer-network/platform-technologies/fbx-sdk-2016-1-2
    wget -O "fbx.tar.gz" "http://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_linux.tar.gz" && \
    mkdir -p fbx && \
    tar xf "fbx.tar.gz" --directory="fbx" && \
    chmod +x fbx/fbx20161_2_fbxsdk_linux && \
    mkdir -p /usr/fbxsdk && \
    echo "yes\nno\nn\n" | fbx/fbx20161_2_fbxsdk_linux /usr/fbxsdk \
    && \
# PDAL
# https://pdal.io/development/compilation/unix.html
# https://github.com/CloudCompare/CloudCompare/blob/master/BUILD.md#optional-setup-for-las-using-pdal
    mkdir -p /tmp/PDAL && \
    cd /tmp/PDAL && \
    git init && \
    git remote add origin https://github.com/PDAL/PDAL.git && \
    git fetch --tags && \
    latestTag=$(git describe --tags `git rev-list --tags --max-count=1`) && \
    cd ${BUILD_ROOT} && rm -rf /tmp/PDAL && \
    git clone --branch $latestTag --depth 1 https://github.com/PDAL/PDAL.git PDAL \
    && \
    mkdir PDAL/build && \
    cd PDAL/build && \
    cmake -G "Unix Makefiles" -H${BUILD_ROOT}/PDAL -B${BUILD_ROOT}/PDAL/build \
        -DCMAKE_BUILD_TYPE=Release \
        -DWITH_TESTS=OFF \
        -DWITH_COMPLETION=ON \
        -DWITH_LASZIP=ON \
        -DBUILD_PLUGIN_PYTHON=ON \
        -DBUILD_PLUGIN_PGPOINTCLOUD=ON \
        # https://github.com/PDAL/PDAL/blob/2.0.1/plugins/CMakeLists.txt
        -DBUILD_PLUGIN_SQLITE=ON \
        -DFBX_INCLUDE_DIRS=/usr/fbxsdk/include \
        -DFBX_LIBRARIES=/usr/fbxsdk/lib/gcc4/x64/release \
        -DBUILD_PLUGIN_FBX=ON \
        -DBUILD_PLUGIN_E57=ON \
    && make && \
    make install \
    && \
# PCL
    apt-get install -y libpcl-dev \
    && \
    /sbin/ldconfig -v \
    && \
# build info and cleanup
    apt-get -y autoremove && \
    apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
    rm -rf /opt/sources && \
    echo "Timestamp:" `date --utc` | tee /image-build-info.txt

WORKDIR /data