FROM opencpu/rstudio

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

ADD ./sources.list /etc/apt/sources.list

Run apt update &&\
    apt upgrade -y \
    && apt-get install -y --no-install-recommends \
    libcairo2-dev \
    librsvg2-dev \
    libmariadb-client-lgpl-dev \
    libxt-dev \
    libxml2 \
    gdebi-core \
    sqlite3 \
    libsqlite3-dev \
    vim \
    libxt-dev \
    pandoc \
    pandoc-citeproc \
    texinfo \
    texlive-base \
	texlive-extra-utils \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
	texlive-latex-base \
	texlive-latex-extra \
	texlive-latex-recommended \
    protobuf-compiler

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
