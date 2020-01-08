FROM mcr.microsoft.com/dotnet/core/runtime:3.1

RUN apt-get update                                                                                                                            \
 && apt-get install -y --no-install-recommends                                                                                                \
                   gnupg                                                                                                                      \
                   apt-transport-https                                                                                                        \
                   software-properties-common                                                                                                 \
                   gcc                                                                                                                        \
                   g++                                                                                                                        \
                   meson                                                                                                                      \
                   python3-pip                                                                                                                \
                   wget                                                                                                                       \
 && pip3 install six
