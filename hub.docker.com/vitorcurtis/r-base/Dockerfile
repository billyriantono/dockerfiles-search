# Copyright (c) 2018, Instituto Tecnológico de Aeronáutica - Divisão de Ciência da Computação
#
# All rights reserved.
# Distributed under the terms of the Modified BSD License (BSD 3-Clause License).
#

FROM vitorcurtis/clang

LABEL maintainer="Vitor Curtis <curtis@ita.br>"



USER root

# Chrome and Firefox browsers
RUN apt-get update && \
	apt-get install -y r-base



USER $NB_UID
