FROM cspicer/vim:vim-plug
MAINTAINER Chris Spicer <git@cspicer.net>

ENV TERM screen-256color
ENV VIMRC_URL "https://raw.githubusercontent.com/cspicer/dotfiles/master/vim/.vimrc"

RUN curl \
    --silent \
    --show-error \
    --location "$VIMRC_URL" \
    --output "$HOME/.vimrc" \
  && vim -c "PlugInstall | qa!"

ENTRYPOINT ["vim"]

