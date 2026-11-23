FROM us-west2-docker.pkg.dev/shared-pub-buckets-94mvrf/workbench-artifacts/app-aou-jupyter@sha256:ce8c0e0cfc166a3fe196ea4cfdef83e83d694f8887ba1c8707345d5b6395a219

COPY --from=extension-builder --chown=$JUPYTER_USER \
    /dist/snippets $JUPYTER_USER_HOME_DIR/.local/share/jupyter/snippets

# Install all extensions we built
RUN --mount=type=bind,from=extension-builder,source=/dist,target=/tmp/extensions \
    /tmp/extensions/setup.sh

COPY --from=load-envs --chown=$JUPYTER_USER \
    /dist/load-env /dist/load-env.sh $JUPYTER_USER_HOME_DIR

RUN echo "source $JUPYTER_USER_HOME_DIR/load-env.sh" >> $JUPYTER_USER_HOME_DIR/.bashrc

# TODO(PHP-87353): Add remotefuse back. See https://github.com/verily-src/workbench-app-devcontainers/pull/227
