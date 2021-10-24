FROM ubuntu:18.04

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=America/Bogota
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes
RUN mkdir /vsts_agent
RUN apt-get update \
&& apt-get -y install tzdata
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
        libcurl4 \
        libicu60 \
        libunwind8 \
        netcat \
        software-properties-common \
        wget \
	unzip \
        apt-transport-https \
        gnupg-agent \
        zip \
        cron \
        vim \
        groovy \
        file \
        python-requests \
&& apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
&& localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
&& apt-get update \
&& apt-get update && apt-get install -y apt-transport-https \
&& curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
&& echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list \
&& apt-get update \
&& apt-get install -y kubectl \
&& curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
&& add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable" \
&& apt-get update \
&& apt-get install -y --allow-unauthenticated docker-ce docker-ce-cli containerd.io \
&& curl -sL https://deb.nodesource.com/setup_12.x -o /opt/nodesource_setup.sh \
&& chmod +x /opt/nodesource_setup.sh \
&& /opt/nodesource_setup.sh \
&& apt-get install nodejs \
&& apt-get update \
&& apt-get install groff \
&& apt-get clean --dry-run \
&& mkdir /devops \
&& mkdir /devops/tools \ 
&& mkdir /devops/tools/k8-cli \
&& ln -s /usr/bin/kubectl /devops/tools/k8-cli/kubectl \
&& apt-get -y update \
&& wget -O /tmp/helm-v3.5.0-linux-amd64.tar.gz https://get.helm.sh/helm-v3.5.0-linux-amd64.tar.gz \
&& tar -zxvf /tmp/helm-v3.5.0-linux-amd64.tar.gz -C /tmp \
&& mv /tmp/linux-amd64/helm /usr/local/bin/helm \
&& rm -rf /tmp/helm-v3.5.0-linux-amd64.tar.gz

WORKDIR /vsts_agent
COPY ./start.sh .
RUN chmod +x start.sh
CMD ["./start.sh"]
