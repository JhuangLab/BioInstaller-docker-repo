FROM opencpu/rstudio

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

ADD ./sources.list /etc/apt/sources.list 
ADD http://bioinfo.rjh.com.cn/download/bioinstaller/shiny-server/shiny-server-1.5.7.907-amd64.deb /tmp/shiny-server-1.5.7.907-amd64.deb

Run apt-get update && apt-get install -y --no-install-recommends \
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
    && echo "options('repos' = c(CRAN='https://mirrors.tuna.tsinghua.edu.cn/CRAN/'))" >> ~/.Rprofile \
    && echo "options(BioC_mirror='https://mirrors.tuna.tsinghua.edu.cn/bioconductor')" >> ~/.Rprofile \
    && Rscript -e "install.packages(c('Rcpp'))" \
    && Rscript -e "install.packages(c('reshape2'))" \
    && Rscript -e "install.packages(c('dplyr'))" \
    && Rscript -e "install.packages(c('stringi', 'stringr', 'ggplot2', 'igraph'))" \
    && Rscript -e "source('https://bioconductor.org/biocLite.R');biocLite(ask = FALSE);" \
    && Rscript -e "install.packages(c('configr', 'ngstk', 'BioInstaller', 'annovarR'))" \
    && Rscript -e "update.packages(ask = FALSE)" \
    && gdebi -n /tmp/shiny-server-1.5.7.907-amd64.deb \
    && echo "shiny-server &" >> /usr/bin/start_shiny_server \
    && chmod a+x /usr/bin/start_shiny_server \
    && a2enmod rewrite\
    && a2enmod proxy_http \
    && a2enmod proxy_wstunnel \
    && chown -R opencpu /var/log/shiny-server \
    && chown -R opencpu /opt/shiny-server \
    && chown -R opencpu /var/lib/shiny-server \
  	&& rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
	&& rm -rf /var/lib/apt/lists/*

CMD service cron start && sh /usr/bin/start_shiny_server && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
