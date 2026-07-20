FROM us-west2-docker.pkg.dev/shared-pub-buckets-94mvrf/workbench-artifacts/app-jupyter-extension-builder@sha256:5e44bbc033cb7c4db588e7882b9fd3605ff5de6d2b5698ba11dba2b44b94f66a

COPY extension /extension

# Original extension is https://github.com/QuantStack/jupyterlab-snippets;
# however, this does not support JupyterLab 4. There is an [open
# PR](https://github.com/QuantStack/jupyterlab-snippets/pull/43) to add
# JupyterLab 4 support, but it has not been merged and seems to be inactive, so
# we'll just build off of the PR branch for now.
ADD https://github.com/darpan097/jupyterlab-snippets.git#a27c8429d2cfaf7aa9e4cad31d3c641d554ac41a /extension/jupyterlab-snippets

RUN /build.sh /extension /dist

COPY snippets /dist/snippets
COPY setup.sh /dist/setup.sh
RUN chmod +x /dist/setup.sh

ENTRYPOINT ["echo", "This image is only a build layer and should not be run directly."]
