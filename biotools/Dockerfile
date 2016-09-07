FROM cbid-base
USER root
# blast
RUN conda install blast=2.2.31

# samtools
RUN conda install samtools=1.3.1

# soapdenovo
ENV ZIP=SOAPdenovo2-bin-LINUX-generic-r240.tgz
ENV URL=https://github.com/BioDocker/software-archive/releases/download/soapdenovo
ENV FOLDER=SOAPdenovo2-bin-LINUX-generic-r240
ENV DST=/tmp

RUN wget $URL/$ZIP -O $DST/$ZIP && \
  tar xvf $DST/$ZIP -C $DST && \
  rm $DST/$ZIP && \
  cd $DST/$FOLDER && \
  mv $DST/$FOLDER/SOAPdenovo* /home/biodocker/bin && \
  cd / && \
  rm -rf $DST/$FOLDER

# bowtie2
ENV ZIP=bowtie2-2.2.9-linux-x86_64.zip
ENV URL=https://github.com/BenLangmead/bowtie2/releases/download/v2.2.9/
ENV FOLDER=bowtie2-2.2.9
ENV DST=/home/biodocker/bin

RUN wget $URL/$ZIP -O $DST/$ZIP && \
    unzip $DST/$ZIP -d $DST && \
    rm $DST/$ZIP && \
    mv $DST/$FOLDER/* $DST && \
    rmdir $DST/$FOLDER

# fastqc
#ENV URL http://www.bioinformatics.babraham.ac.uk/projects/fastqc
#ENV ZIP fastqc_v0.11.5.zip
#ENV FOLDER=fastqc_v0.11.5
#ENV TMP=/tmp
#ENV DST=/home/biodocker/bin

#RUN 	wget $URL/$ZIP -O $TMP/$ZIP && \
#        unzip $DST/$ZIP -d $TMP && \
#	rm $DST/$ZIP && \
#	cd $TMP/$FOLDER && \
#	chmod a+x $TMP/$FOLDER/fastqc && \
#	mv $TMP/$FOLDER/fastqc $DST && \
#	rmdir $TMP/$FOLDER

# pandaseq
#RUN     mkdir tools && \
 #       cd /tools && \
  #      git clone https://github.com/neufeld/pandaseq && \
   #     cd pandaseq && \
    #    ./autogen.sh && \
     #   ./configure && \
     #   make && \
      #  make install && \
       # ldconfig
# Change workdir to /data/
#WORKDIR /data/

# trimmomatic

# samtools
# fastx-toolkit
# hmmr
# DESeq2
# cutadapt
# prinseq-lite
# MOCAT
# diamond



