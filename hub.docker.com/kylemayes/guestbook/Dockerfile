FROM kylemayes/rocket

# Add the project files
ADD . app
WORKDIR app

# Compile the project
RUN cargo build --release

# Run the project
ENV ROCKET_ENV production
ENV ROCKET_PORT 8080
ENTRYPOINT ["./target/release/guestbook"]
