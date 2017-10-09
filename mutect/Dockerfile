FROM anapsix/alpine-java:8

MAINTAINER life2cloud lee_jianfeng@sjtu.edu.cn

ENV version 1.1.7

RUN cd /tmp/ && curl -fsSL https://github.com/Miachol/gatk_releases/raw/master/mutect${version}.tar.gz -o mutect${version}.tar.gz\
        && tar -xzvf mutect${version}.tar.gz \
        && mv /tmp/mutect${version}/mutect-${version}.jar /usr/bin/mutect.jar \
        && rm -rf /var/cache/apk/* \
        && rm -rf /tmp/*

ENTRYPOINT ["java", "-jar", "/usr/bin/mutect.jar"]
