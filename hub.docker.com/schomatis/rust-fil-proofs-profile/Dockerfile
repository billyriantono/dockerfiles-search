# What does this Dockerfile do?
# =============================
#
# It does a memory profile of a PR with `gperftools`.
# TODO: Expand on this.

# Command used:
# ```
# docker --log-level debug build --progress tty --cpuset-cpus 0-1 -t rust-fil-proofs-profile . && docker run -ti rust-fil-proofs-profile
# ```
# or add `bash` at the end to skip the `pprof` and explore.

FROM schomatis/rust-fil-proofs

# `gperftools` and dependencies (`libunwind`)
# -------------------------------------------

ENV GPERFTOOLS_VERSION="2.7"
ENV LIBUNWIND_VERSION="0.99-beta"

ENV HOME="/root"
ENV DOWNLOADS=${HOME}/downloads
RUN mkdir -p ${DOWNLOADS}
RUN echo ${DOWNLOADS} 
WORKDIR ${DOWNLOADS}

RUN wget http://download.savannah.gnu.org/releases/libunwind/libunwind-${LIBUNWIND_VERSION}.tar.gz --output-document ${DOWNLOADS}/libunwind-${LIBUNWIND_VERSION}.tar.gz
RUN tar -xvf ${DOWNLOADS}/libunwind-${LIBUNWIND_VERSION}.tar.gz
WORKDIR ${DOWNLOADS}/libunwind-${LIBUNWIND_VERSION}
RUN ./configure
RUN make
RUN make install
WORKDIR ${DOWNLOADS}

RUN wget https://github.com/gperftools/gperftools/releases/download/gperftools-${GPERFTOOLS_VERSION}/gperftools-${GPERFTOOLS_VERSION}.tar.gz  --output-document ${DOWNLOADS}/gperftools-${GPERFTOOLS_VERSION}.tar.gz
RUN tar -xvf ${DOWNLOADS}/gperftools-${GPERFTOOLS_VERSION}.tar.gz
WORKDIR ${DOWNLOADS}/gperftools-${GPERFTOOLS_VERSION}
RUN ./configure
RUN make install
WORKDIR ${DOWNLOADS}

# Build profile PR
# ----------------

ENV RUST_PROOFS_DIR=${RUST_DIR}/rust-fil-proofs
# TODO: This has been updated in `rust-fil-proofs`.
WORKDIR ${RUST_PROOFS_DIR}

RUN git fetch origin pull/487/head:feat/replicate/reduce-memory-usage
RUN git checkout feat/replicate/reduce-memory-usage

WORKDIR ${RUST_PROOFS_DIR}/filecoin-proofs

ENV CARGO_INCREMENTAL=1
RUN cargo build --release --example zigzag --features profile,gperftools/heap -v -v

ENV HEAP_PROFILE_MMAP=1
ENV HEAP_PROFILE_TIME_INTERVAL=10

# TODO: Check if `HEAPPROFILE` overrides the path set in the code.
ENV HEAPPROFILE_DIR=${HOME}/profiles
RUN mkdir -p ${HEAPPROFILE_DIR}
ENV HEAPPROFILE=${HEAPPROFILE_DIR}/heap.profile

WORKDIR ${RUST_PROOFS_DIR}

ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/lib
# TODO: `gperftools` installs the library (`make install`) in
# `/usr/local/lib` by default but Debian/Ubuntu don't look
# there now, the correct `--prefix` should be added to the
# command.
# TODO: Move up with the install commands.

RUN ./target/release/examples/zigzag --size 1024 --no-bench
# thread '<unnamed>' panicked at 'cannot access stderr during shutdown', src/libcore/option.rs:1008:5
# TODO: What's that?

# Find the last `replicate.profile.XXXX.heap` file
# TODO: We may not want the *last* when we may be already releasing
# memory but rather the one before (or the one before that).
RUN find . -maxdepth 1 -name 'replicate.profile.[0-9]*.heap' | \
      sed 's/\.\/replicate\.profile\.\([0-9][0-9]*\)\.heap/\1/' | \
      sort -n | \
      tail -n 1 > max-profile
      # TODO: Can't save it in an env.var like `MAX_PROFILE=$(find...)`.

CMD pprof --inuse_space ./target/release/examples/zigzag replicate.profile.$(cat max-profile).heap
