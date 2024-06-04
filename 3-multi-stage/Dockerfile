FROM ghcr.io/prefix-dev/pixi:0.23.0 AS build

WORKDIR /app
COPY . .
RUN pixi install --locked
RUN pixi shell-hook -s bash > /entrypoint.sh
RUN echo "uvicorn my_project:app --host 0.0.0.0" >> /entrypoint.sh

FROM ubuntu:24.04 AS production
WORKDIR /app
COPY --from=build /app/.pixi/envs/default /app/.pixi/envs/default
COPY --from=build /entrypoint.sh /entrypoint.sh
COPY ./my_project /app/my_project
EXPOSE 8000
CMD ["bash", "/entrypoint.sh"]
