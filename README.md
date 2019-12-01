# Recursive sed transformer

This is a plugin for kustomize that transforms output from `kustomize build` and processes it using sed scripts.
The script looks for `script.sed` files in a recursive way - starting from the directory with kustomization overlay, going up directory tree unit it reaches root directory /.

# Use cases

- Easily replace hostnames in ingress (see example; this is why I invented the plugin)
- Replace values inside config maps
- Replace values inside files generated with config map geneators or secret generators

# Usage

For dev env execute:
```
cd example/prod/test-service
kustomize_3.1.0_linux_amd64 build --enable_alpha_plugins --load_restrictor none
```
And observe that `dev/script.sed` was applied.

For prod execute:
```
cd example/dev/test-service
kustomize_3.1.0_linux_amd64 build --enable_alpha_plugins --load_restrictor none
```
And observe that both `prod/script.sed` and `prod/test-service/script.sed` were applied.