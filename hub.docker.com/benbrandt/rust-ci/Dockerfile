FROM rust:1.40.0

# Install cargo tools
RUN cargo install cargo-cache; \
    cargo install cargo-audit; \
    cargo install diesel_cli; \
    # Cleanup unneeded registry files
    cargo cache --autoclean;
