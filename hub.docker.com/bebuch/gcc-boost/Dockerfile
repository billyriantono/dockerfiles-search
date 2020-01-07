FROM bebuch/gcc-gtest:latest

MAINTAINER Benjamin Buch <https://github.com/bebuch-docker/gcc-boost>


# install dependencies
ENV \
	BOOST_MAJOR=1 \
	BOOST_MINOR=67 \
	BOOST_PATCH=0 \
	BOOST_ROOT=/opt/boost
ENV \
	BOOST_VERSION=${BOOST_MAJOR}.${BOOST_MINOR}.${BOOST_PATCH} \
	BOOST_DIR=boost_${BOOST_MAJOR}_${BOOST_MINOR}_${BOOST_PATCH} \
	LD_LIBRARY_PATH=/usr/local/lib \
	PATH=$PATH:$BOOST_ROOT
RUN cd /opt \
	&& curl "https://dl.bintray.com/boostorg/release/$BOOST_VERSION/source/$BOOST_DIR.tar.bz2" -L --output $BOOST_DIR.tar.bz2 --silent \
	&& tar xjf $BOOST_DIR.tar.bz2 \
	&& rm $BOOST_DIR.tar.bz2 \
	&& ln -s /opt/$BOOST_DIR /opt/boost \
	&& cd $BOOST_ROOT \
	&& ./bootstrap.sh \
	&& bjam -j 2 --build-type=complete --layout=versioned stage \
	&& bjam install
