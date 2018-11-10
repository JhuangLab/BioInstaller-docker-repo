FROM opencpu/rstudio

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

ADD https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.9.923-amd64.deb /tmp/shiny-server.deb
ADD ./sources.list /etc/apt/sources.list

Run apt update \
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
    protobuf-compiler \
    r-base\
    && echo "options('repos' = c(CRAN='https://mirrors.tuna.tsinghua.edu.cn/CRAN/'))" >> ~/.Rprofile \
    && echo "options(BioC_mirror='https://mirrors.tuna.tsinghua.edu.cn/bioconductor')" >> ~/.Rprofile \
    && Rscript -e "update.packages(ask = FALSE, checkBuilt=TRUE)" \
    && runuser -s /bin/bash -l opencpu -c 'Rscript -e "update.packages(ask = FALSE, checkBuilt=TRUE)"' \
    && Rscript -e "install.packages('pacman')" \
    && Rscript -e "install.packages('BiocManager');BiocManager::install();" \
    && Rscript -e "pacman::p_load(jsonlite, rvcheck, Rcpp, reshape2, dplyr)" \
    && Rscript -e "pacman::p_load(stringi, stringr, ggplot2, igraph)" \
    && Rscript -e "pacman::p_load(configr, ngstk, BioInstaller, annovarR)" \
    && Rscript -e "rvcheck::update_all()" \
    && Rscript -e "BiocManager::install(ask = FALSE, update = TRUE)" \
    && gdebi -n /tmp/shiny-server.deb \
    && echo "shiny-server &" >> /usr/bin/start_shiny_server \
    && chmod a+x /usr/bin/start_shiny_server \
    && a2enmod rewrite\
    && a2enmod proxy_http \
    && a2enmod proxy_wstunnel \
    && chown -R opencpu /var/log/shiny-server \
    && chown -R opencpu /opt/shiny-server \
    && chown -R opencpu /var/lib/shiny-server \
  	&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds \

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
