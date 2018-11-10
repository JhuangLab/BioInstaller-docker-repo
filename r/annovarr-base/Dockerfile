FROM bioinstaller/opencpu:latest

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

Run Rscript -e "devtools::install_github('Miachol/configr', ref = 'develop')" \
    && Rscript -e "devtools::install_github('JhuangLab/ngstk', ref = 'develop')" \
    && Rscript -e "devtools::install_github('JhuangLab/BioInstaller', ref = 'develop')" \
    && Rscript -e "devtools::install_github('JhuangLab/annovarR', ref = 'develop')" \ 
    && ln -s /usr/local/lib/R/site-library/annovarR/extdata/tools/shiny/R /srv/shiny-server/annovarR \
    && mkdir -p /home/opencpu/.annovarR/tools/ \
    && mkdir -p /home/opencpu/.annovarR/db/ \
    && chown -R opencpu /home/opencpu/.annovarR \
    && echo 'LC_ALL="en_US.UTF-8"\nLANG="en_US.UTF-8"' >> /etc/R/Renviron \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && rm -rf /var/lib/apt/lists/* \
    && rm /etc/apache2/sites-enabled/rstudio.conf

ADD https://raw.githubusercontent.com/JhuangLab/annovarR/master/inst/docker/shiny-server.conf /etc/shiny-server/shiny-server.conf
ADD https://raw.githubusercontent.com/JhuangLab/annovarR/master/inst/docker/shiny-apache.conf /etc/apache2/sites-enabled/000-default.conf

ADD https://github.com/brentp/vcfanno/releases/download/v0.3.1/vcfanno_linux64 /home/opencpu/.annovarR/tools/vcfanno
ADD http://www.openbioinformatics.org/annovar/download/0wgxR2rIVP/annovar.{{version}}.tar.gz /home/opencpu/.annovarR/tools/annovar.latest.tar.gz

RUN cd /home/opencpu/.annovarR/tools/ && tar -xzvf annovar.latest.tar.gz \
    && rm annovar.latest.tar.gz && chown -R opencpu /home/opencpu/.annovarR \
    && chmod a+x /home/opencpu/.annovarR/tools/vcfanno \
    && chmod a+r /etc/shiny-server/shiny-server.conf

RUN ln -s /home/opencpu/.annovarR/tools/annovar/humandb/* /home/opencpu/.annovarR/db

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
