# syntax=docker/dockerfile:1.0-experimental

#define base image; replace with your image location once hardened
FROM opensuse/leap:latest

#define maintainer 
LABEL maintainer="mmoalzahrani@tahakom.com"

#define version
LABEL version="V1"

# create a directory to work in
RUN mkdir udacity \
    && cd udacity

# Remove inexist repo
RUN zypper rr http://download.opensuse.org/update/leap/15.4/sle/

#install zypper 
RUN zypper refs && zypper refresh

#add local user
USER $SEC_USER
