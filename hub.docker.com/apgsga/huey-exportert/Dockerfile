FROM alpine:3.9

# We need GCC to build our tools
# GDB will allow us to debug programs we build
# The Alpine Linux base iamge uses musl as its C runtime library
# Make lets us orchestrate building components easily

RUN apk add gcc gdb musl-dev make

