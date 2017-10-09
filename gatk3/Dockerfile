FROM anapsix/alpine-java:8

MAINTAINER life2cloud lee_jianfeng@sjtu.edu.cn

ENV version 3.8-0

RUN cd /tmp/ && curl -fsSL https://github.com/Miachol/gatk_releases/raw/master/gatk${version}.tar.gz -o gatk${version}.tar.gz \
        && tar -xzvf gatk${version}.tar.gz \
        && mv /tmp/gatk${version}/GenomeAnalysisTK.jar /usr/bin/ \
        && rm -rf /var/cache/apk/* \
        && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/bin/GenomeAnalysisTK.jar"]
