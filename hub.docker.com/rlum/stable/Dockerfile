FROM rlum/core

MAINTAINER "Christoph Burow" christoph.burow@gmx.net

RUN . /etc/environment \
	&& echo "R_LIBS_USER='/usr/lib/R/site-library'" >> /usr/local/lib/R/etc/Renviron \
	&& echo "R_LIBS=\${R_LIBS-'/usr/lib/R/site-library:/usr/local/lib/R/library'}" >> /usr/local/lib/R/etc/Renviron \
	&& install2.r --error -l "/usr/lib/R/site-library/" \
		--repos "https://mran.microsoft.com/" \
		--deps "TRUE" \
		Luminescence RLumModel RLumShiny