FROM cspicer/vim:base
MAINTAINER Chris Spicer <git@cspicer.net>

ENV VIM_PLUG_URL "https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim"

RUN apt-get update -qq \
  && apt-get install -y \
    git \
    curl \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y

RUN curl \
    --silent \
    --show-error \
    --create-dirs \
    --location "$VIM_PLUG_URL" \
    --output "$HOME/.vim/autoload/plug.vim" \
  && echo "call plug#begin()" >> "$HOME/.vimrc" \
  && echo "call plug#end()" >> "$HOME/.vimrc" \
  && vim -c "PlugInstall | qa!"

ENTRYPOINT ["vim"]
