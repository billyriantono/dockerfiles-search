# Base image
FROM codereaper91/gcc:8.3.0

# Copy cross compilers
COPY --from=codereaper91/crossdev-i686-elf:8.3.0 /opt/cross /opt/cross
COPY --from=codereaper91/crossdev-arm-none-eabi:8.3.0 /opt/cross /opt/cross

## Environment
ENV CROSS_COMPILER="/opt/cross"
ENV PATH="${CROSS_COMPILER}/bin:${PATH}"

### Default values
ENV TARGET=i686-elf
