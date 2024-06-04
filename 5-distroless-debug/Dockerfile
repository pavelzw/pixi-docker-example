FROM ghcr.io/prefix-dev/pixi:0.23.0-bookworm AS build

WORKDIR /app
COPY . .
RUN pixi install --locked -e prod

FROM gcr.io/distroless/base-debian12:debug AS production
WORKDIR /app
COPY --from=build /app/.pixi/envs/prod /app/.pixi/envs/prod
COPY ./my_project /app/my_project
EXPOSE 8000
# from pixi shell-hook -e prod
# add a /busybox to the PATH, otherwise you can't run any commands
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/busybox
ENV CONDA_PREFIX=/app/.pixi/envs/default
CMD ["/app/.pixi/envs/prod/bin/uvicorn", "my_project:app", "--host", "0.0.0.0"]