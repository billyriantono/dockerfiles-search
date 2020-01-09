# Create a base docker container that can execute FSL commands
#
# Example usage:
#   docker run --rm -ti \
#       mcin/fsl-v5.0 <fsl_command> <input_arguments>
#

# Start with neurodebian image
FROM neurodebian:wheezy

# Run apt-get calls
RUN echo 'deb http://neurodeb.pirsquared.org data main contrib non-free'   >> /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo 'deb http://neurodeb.pirsquared.org wheezy main contrib non-free' >> /etc/apt/sources.list.d/neurodebian.sources.list
RUN apt-get update \
    && apt-get install -y fsl-5.0-core

# Configure environment
ENV FSLDIR=/usr/lib/fsl/5.0
ENV FSLOUTPUTTYPE=NIFTI_GZ
ENV PATH=$PATH:$FSLDIR
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$FSLDIR
ENV FSLMULTIFILEQUIT=TRUE
ENV POSSUMDIR=/usr/share/fsl/5.0
ENV FSLTCLSH=/usr/bin/tclsh
ENV FSLWISH=/usr/bin/wish

# Run configuration script for normal usage
RUN echo ". /etc/fsl/5.0/fsl.sh" >> /root/.bashrc

