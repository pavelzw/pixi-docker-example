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
ENV PATH=/app/.pixi/envs/prod/bin:$PATH
ENV CONDA_PREFIX=/app/.pixi/envs/prod
ENTRYPOINT []
CMD [ "uvicorn", "my_project:app", "--host", "0.0.0.0" ]
