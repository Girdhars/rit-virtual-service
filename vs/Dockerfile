# Generated from project topology discovery
FROM ubuntu:14.04

# ------------------------------------------------------------------------------------
# All lines below should be left unchanged unless otherwise stated
# ------------------------------------------------------------------------------------ 

RUN apt-get update \
  && apt-get install --no-install-recommends -y wget unzip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/*

ENV RITC_VERSION=ritc-se_9101 \
   RITC_REPO=ftp://public.dhe.ibm.com/software/spcn/continuoustest/docker \
   TINI_VERSION=v0.9.0

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini

RUN wget -nv ${RITC_REPO}/${RITC_VERSION}.zip#I20170626_1422 \
  && unzip -q ${RITC_VERSION}.zip \
  && rm ${RITC_VERSION}.zip

# ------------------------------------------------------------------------------------
# To change the locale, replace the RIT_LOCALE value in the following line
# ------------------------------------------------------------------------------------
ENV RIT_LOCALE=en_US

ENV LANG=${RIT_LOCALE}.UTF-8 \
   LC_ALL=${RIT_LOCALE}.UTF-8 \
   LANGUAGE=${RIT_LOCALE}:

RUN locale-gen "${RIT_LOCALE}.UTF-8"

COPY /UserLibs /UserLibs
COPY /Project /Project
COPY /stubs.info /stubs.info

# Stub VS1 is exposed on port 8088/TCP
EXPOSE 8088

ENTRYPOINT ["/bin/tini", "--", "/IntegrationTester/RunTests", "-project", "/Project/topology discovery.ghp", "-environment", "GIRDHARS04", "-noHTTP", "-run", "-798ad0f4:15e6fcc3994:-7edb", "-environmentTags", "env" ]
