FROM jorizci/azkaban-executor:3.30.1
MAINTAINER Jorge Izquierdo Ciges <jorizci@ebi.com>

# Install Plink
RUN wget https://www.cog-genomics.org/static/bin/plink170815/plink_linux_x86_64.zip \
    && unzip plink_linux_x86_64.zip -d /opt/plink \
    && rm plink_linux_x86_64.zip 

ENV PATH="/opt/plink/:${PATH}"

# Install Oxford pipeline scripts
ADD ./pipeline_exclusion/run_pipeline_exclusion.sh /opt/scripts/pipeline_exclusion/
ADD ./pipeline_exclusion/01.pipeline/* /opt/scripts/pipeline_exclusion/01.pipeline/

ENV PATH="/opt/scripts/pipeline_exclusion/:${PATH}"
