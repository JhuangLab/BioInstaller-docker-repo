FROM bioinstaller/opencpu:latest

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

Run Rscript -e "devtools::install_github('JhuangLab/BioInstaller')" \
    && ln -s /usr/local/lib/R/site-library/BioInstaller/extdata/shiny/ /srv/shiny-server/BioInstaller \
    && mkdir /home/opencpu/.BioInstaller \
    && chown -R opencpu /home/opencpu/.BioInstaller \
    && echo 'LC_ALL="en_US.UTF-8"\nLANG="en_US.UTF-8"' >> /etc/R/Renviron \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && rm -rf /var/lib/apt/lists/* \
    && rm /etc/apache2/sites-enabled/rstudio.conf

Run Rscript -e "source(system.file('extdata', 'shiny/deps.R', package = 'BioInstaller'))"

ADD https://raw.githubusercontent.com/JhuangLab/annovarR/master/inst/docker/shiny-server.conf /etc/shiny-server/shiny-server.conf
ADD https://raw.githubusercontent.com/JhuangLab/annovarR/master/inst/docker/shiny-apache.conf /etc/apache2/sites-enabled/000-default.conf

RUN chmod a+r /etc/shiny-server/shiny-server.conf

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
