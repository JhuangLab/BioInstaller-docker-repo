FROM opencpu/rstudio

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@openbiox.org

ENV bioc_version devel

ADD ./sources.list /etc/apt/sources.list

Run apt update \
    && apt upgrade -y \
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


Run Rscript -e "install.packages('BiocManager');BiocManager::install(version = \"${bioc_version}\", ask = FALSE);" \
    && Rscript -e "BiocManager::install('AnnotationDbi', version = \"${bioc_version}\", ask = FALSE)" \
    && Rscript -e "install.packages(c('rvcheck', 'rmarkdown', 'testthat', 'roxygen2'))" \
    && echo 'source /etc/profile' >> /home/opencpu/.bashrc \
    && echo 'source /etc/profile' >> /root/.bashrc

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
