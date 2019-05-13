FROM bioinstaller/opencpu-base

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

ENV bioc_version devel

Run Rscript -e "install.packages('BiocManager');BiocManager::install(version = \"${bioc_version}\", ask = FALSE);" \
    && Rscript -e "BiocManager::install('AnnotationDbi', version = \"${bioc_version}\", ask = FALSE)" \
    && Rscript -e "BiocManager::install('maftools', version = \"${bioc_version}\", ask = FALSE)" \
    && Rscript -e "BiocManager::install('clusterProfiler', version = \"${bioc_version}\", ask = FALSE)" \
    && echo 'source /etc/profile' >> /home/opencpu/.bashrc \
    && echo 'source /etc/profile' >> ~/.bashrc

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
