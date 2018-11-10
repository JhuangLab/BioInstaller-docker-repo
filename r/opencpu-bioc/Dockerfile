FROM bioinstaller/opencpu-base

## This handle reaches Jianfeng
MAINTAINER "Jianfeng Li" lee_jianfeng@life2cloud.com

Run Rscript -e "install.packages('BiocManager');BiocManager::install();"

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
