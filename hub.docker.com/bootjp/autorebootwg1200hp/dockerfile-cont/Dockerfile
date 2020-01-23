FROM alpine:3.8 as builder
LABEL REPOSITORY="gromacs" \
      maintainer="benjamindoran@alumni.harvard.edu"
ENV GROMACS_VERSION 5.1.2
RUN apk add --no-cache cmake g++ libxml2 make perl \
	&& wget ftp://ftp.gromacs.org/pub/gromacs/gromacs-${GROMACS_VERSION}.tar.gz
RUN tar zxfv gromacs-${GROMACS_VERSION}.tar.gz \
	&& mkdir "./gromacs-${GROMACS_VERSION}/build/"
WORKDIR "./gromacs-${GROMACS_VERSION}/build"
RUN cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=ON \
	&& make \
	&& make check \
	&& make install
WORKDIR "/"

FROM alpine:3.8 as app
RUN apk add --no-cache bash g++
COPY --from=builder /usr/local/gromacs /usr/local/gromacs
ENV PATH "/usr/local/gromacs/bin:${PATH}"
CMD ["gmx", "-version"]
