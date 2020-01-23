FROM golang:latest

# Add Maintainer Info
LABEL maintainer="Matt Kimberley <mattkimberley84@gmail.com>"

COPY src/ /app

WORKDIR /app

# Build the Go app
RUN go build main.go

# Expose port 8080 to the outside world
EXPOSE 8080

# Command to run the executable
CMD ["./main"]