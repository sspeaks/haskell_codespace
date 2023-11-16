FROM nixos/nix:latest

WORKDIR haskell

COPY . .

RUN nix-env -i direnv &&  echo "eval \"\$(direnv hook bash)\"" > ~/.bashrc
RUN direnv allow && nix-shell
