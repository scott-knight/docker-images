FROM ruby:slim as build

LABEL maintainer="dc.sknight@gmail.com"

RUN apt-get update -qq && apt-get -y --no-install-recommends install\
  build-essential\
  curl\
  git\
  libpq-dev\
  libssl-dev \
  libxml2-dev\
  libxslt1-dev\
  sudo\
  vim\
  zsh\
  && apt -y autoremove \
  && rm -rf /root/.cpanm /root/.rpmdb /tmp/* /var/lib/apt/lists/*

# NODE AND YARN
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get update -qq && apt-get -yq dist-upgrade && apt-get -y --no-install-recommends install\
  nodejs\
  && apt -y autoremove \
  && rm -rf /root/.cpanm /root/.rpmdb /tmp/* /var/lib/apt/lists/*
RUN npm install npm@latest -g
RUN npm install --global yarn

ENV HOME=/root

# setup the env
RUN cd $HOME &&\
  sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" &&\
  git clone https://github.com/zsh-users/zsh-autosuggestions $HOME/.oh-my-zsh/custom/plugins/zsh-autosuggestions &&\
  git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $HOME/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
RUN cd $HOME && npm install -g spaceship-zsh-theme

RUN rm -rf $HOME/.zshrc
COPY ${pwd}/.* $HOME

# Make Dirs
RUN mkdir -p /bundle
RUN mkdir -p /yarn_cache
RUN mkdir -p /app

# SYSTEM ENVs
ENV LANG=en_US.UTF-8 \
  BUNDLE_RETRY=3\
  BUNDLE_PATH=/bundle\
  EDITOR=vim\
  PORT=3000\
  YARN_CACHE_FOLDER=/yarn_cache
EXPOSE $PORT

WORKDIR /app

# Install multiple gems at the same time
RUN bundle config set jobs 4
RUN gem update --system
RUN gem update bundler rake

CMD ["zsh"]