## Dockerized  [bwa](http://https://github.com/life2cloud/BioInstaller-docker-repo/bwa/)

### Usage:

Docker Pull Command:

```
docker pull life2cloud/bwa
```

Example (bwa mem for paired-end Illumina reads):

```
docker run --rm -it -v  ~/reference:/reference -v $(pwd):/data life2cloud/bwa mem -M -t 8 reference/reference /data/1.fastq /data/2.fastq  > mapping.sam
```
