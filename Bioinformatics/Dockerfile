FROM gitpod/workspace-full
ENV PATH="/opt/conda/bin:$PATH"
ARG PATH="/opt/conda/bin:$PATH"

# update package manager and install dependencies
RUN sudo apt-get update    
RUN echo 'debconf debconf/frontend select Noninteractive' | sudo debconf-set-selections
# install ncbi blast
RUN sudo apt-get install -y ncbi-blast+
# install samtools
RUN sudo apt-get install -y samtools

# install muscle
RUN sudo apt-get install -y muscle emboss mafft velvet bowtie2 bwa trinityrnaseq

RUN mkdir /home/gitpod/.conda 
# Install conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    sudo /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    sudo ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc
    
 
RUN sudo chown -R gitpod:gitpod /opt/conda \
    && sudo chmod -R 777 /opt/conda \
    && sudo chown -R gitpod:gitpod /home/gitpod/.conda \
    && sudo chmod -R 777 /home/gitpod/.conda
RUN conda install -y  -c conda-forge mamba
RUN mamba create -n busco -y  -c conda-forge -c bioconda busco


# Clean up
RUN sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

