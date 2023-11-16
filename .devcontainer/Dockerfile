FROM ubuntu:latest

RUN apt update && apt -y install sudo xz-utils curl

WORKDIR haskell

COPY . .

RUN sudo install -d -m755 -o $(id -u) -g $(id -g) /nix
RUN groupadd -r nixbld
RUN for n in $(seq 1 10); do useradd -c "Nix build user $n" \
    -d /var/empty -g nixbld -G nixbld -M -N -r -s "$(which nologin)" \
    nixbld$n; done 
RUN curl -L https://nixos.org/nix/install | sh
ENV PATH="${PATH}:/root/.nix-profile/bin"
RUN nix-env -i direnv &&  echo "eval \"\$(direnv hook bash)\"" > ~/.bashrc
RUN direnv allow && nix-shell
