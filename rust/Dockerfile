FROM alpine:3.16.2

ENV RUNNING_IN_DOCKER true

# Setup OS env
RUN adduser -D main && apk --no-cache add zsh curl git g++ make neovim ripgrep fzf
USER main
WORKDIR /home/main

# Setup rust
RUN touch ~/.zshrc && curl https://sh.rustup.rs -sSf | sh -s -- -y

# Setup rust-analyzer
RUN mkdir -p ~/.local/bin \
    && curl -L https://github.com/rust-lang/rust-analyzer/releases/latest/download/rust-analyzer-x86_64-unknown-linux-musl.gz | gunzip -c - > ~/.local/bin/rust-analyzer \
    && chmod +x ~/.local/bin/rust-analyzer \
    && echo "export PATH=\$PATH:\$HOME/.local/bin" >> $HOME/.zshrc

SHELL ["/bin/zsh", "-c"]

# Setup nvim
RUN curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
      https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
COPY init.vim .config/nvim/init.vim

ENTRYPOINT ["/bin/zsh"]

