FROM biocontainers/biocontainers:vdebian-buster-backports_cv1
USER root
RUN apt-get update --fix-missing
RUN apt-get install -t buster-backports -y \
    wget \
    curl \
    git \
    build-essential \
    nano \
    man \
    less \
    bwa \
    samtools

RUN apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/*

# create a non-root user
RUN useradd -ms /bin/bash bioinfo 
WORKDIR /home/bioinfo/alignment/bwa_index
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.dict
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.amb
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.ann
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.bwt
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.fai
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.pac
RUN curl -LO https://storage.googleapis.com/bioinfostudio/alignment/bwa_index/human_g1k_v37.fasta.sa
# setup the user directory
RUN chown -R bioinfo:bioinfo /home/bioinfo
RUN echo 'export PS1=" \W\$ "' >> /home/bioinfo/.bashrc
# become the bioinfo
USER bioinfo
ENV HOME /home/bioinfo
WORKDIR /home/bioinfo/
