FROM ghcr.io/prefix-dev/pixi:0.23.0

WORKDIR /app
COPY . .
RUN pixi install --locked && rm -rf ~/.cache/rattler
EXPOSE 8000
CMD ["pixi", "run", "start"]
