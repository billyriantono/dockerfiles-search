# Docker Image for Vigie Public Demo
FROM scratch

# Specifing the Working Dir is mandatory for relative paths
WORKDIR /app

# Copy our static executable and tests in the Working Dir
COPY . /app/

# Run the Vigie binary
ENTRYPOINT ["/app/vigie", "run", "--config" ,"/app/config/vigie-demo.toml"]