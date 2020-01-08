FROM rainbean/tensor:latest as builder
ADD . /src
WORKDIR /src
RUN python setup.py bdist_egg --exclude-source-files

FROM rainbean/tensor:latest
LABEL maintainer "Jimmy Lee"
RUN apt-get update && apt-get install -y --no-install-recommends \
    openslide-tools python3-openslide && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
WORKDIR /mnt
COPY --from=builder /src/dist/* .
RUN python -m easy_install ./*.egg
ENTRYPOINT ["python", "-m", "cyto_classifier"]
