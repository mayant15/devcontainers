FROM ubuntu:kinetic

ENV RUNNING_IN_DOCKER true

# Setup OS env
RUN useradd -s /bin/bash main && apt update && apt install -y zsh curl git neovim ripgrep fzf

USER main
WORKDIR /home/main

SHELL ["/bin/zsh", "-c"]

# Setup TypeScript
RUN touch ~/.zshrc \
    && (curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash) \
    && source ~/.zshrc \
    && nvm install node \
    && nvm alias default node \
    && npm i -g typescript typescript-language-server yarn

# Setup nvim
RUN curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
      https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
COPY init.vim .config/nvim/init.vim

ENTRYPOINT ["/bin/zsh"]

