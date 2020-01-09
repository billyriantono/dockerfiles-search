# -*- coding: utf-8 -*-
#
# =============================================================================
#
# MIT License
#
# Copyright (c) 2018 Andre Richter <andre.o.richter@gmail.com>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# =============================================================================
FROM buildpack-deps:stretch

LABEL version="1.0"
LABEL author="Andre Richter" email="andre.o.richter@gmail.com"
LABEL author="Andrew Hu" email="andrew.n.hu.87@gmail.com"

RUN git clone https://github.com/qemu/qemu.git; \
    cd qemu; \
    git checkout stable-2.12; \
    ./configure --target-list=aarch64-softmmu --enable-modules \
        -enable-tcg-interpreter --enable-debug-tcg; \
    make -j4; \
    make install; \
    cd ..; \
    rm -rf qemu

RUN git clone https://github.com/andre-richter/raspbootin.git; \
    cd raspbootin/raspbootcom; \
    make; \
    cp raspbootcom /usr/bin; \
    cd ../..; \
    rm -rf raspbootin
