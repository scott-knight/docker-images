# Dockerfile
# Builder Stage
FROM ruby:3.0-slim as build

LABEL maintainer="dc.sknight@gmail.com"

RUN apt-get update -qq && apt-get install -y\
  nodejs\
  postgres-client\
  && rm -rf /var/lib/apt/lists/*

RUN apk update && apk --no-cache add --update --virtual \
runtime-deps \
build-base \
bash \
ca-certificates \
coreutils \
curl \
file \
git \
nodejs-current \
npm \
npm-bash-completion \
openssl \
zlib-dev \
libxml2-dev \
libxslt-dev \
# Postgres
postgresql-client \
postgresql-dev \
# Images
imagemagick \
vips \
# HTML to PDF conversion
# ttf-ubuntu-font-family \
# wkhtmltopdf \
libstdc++ \
libffi-dev \
libc-dev \
libnotify-dev \
linux-headers \
readline \
readline-dev \
rsync \
shared-mime-info \
tzdata \
vim \
zsh \
&& rm -rf /var/cache/apk/*

# Set APP ENVs
ENV BUNDLE_PATH /bundle
ENV YARN_CACHE_FOLDER /yarn_cache

RUN mkdir -p $YARN_CACHE_FOLDER

# SYSTEM ENVs
ENV EDITOR vim
ENV LANG en_US.UTF-8
ENV PORT 3000

EXPOSE $PORT

RUN npm install --global yarn

# Install multiple gems at the same time
RUN bundle config set jobs $(nproc)
RUN gem update --system
RUN gem update bundler rake