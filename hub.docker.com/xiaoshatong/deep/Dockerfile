FROM floydhub/dl-docker:gpu

# Install some dependencies
RUN apt-get update && apt-get install -y \
        tree \
		&& \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*
# Link BLAS library to use OpenBLAS using the alternatives mechanism (https://www.scipy.org/scipylib/building/linux.html#debian-ubuntu)


# Install other useful Python packages using pip
RUN pip --no-cache-dir install \
        autosub \
        face_recognition
