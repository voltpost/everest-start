Approximate the EVerest [Quickstart](https://everest.github.io/nightly/general/03_quick_start_guide.html).

## Actions workflow
- Build the devcontainer so we can run the build inside it.
- Run `edm init`.
- Run CMake.
- Run Ninja.

## Running the devcontainer locally
First you must have a GitHub personal access token. Then you can use the token as a password to log into GitHub Container registry.
```shell
docker login ghcr.io -p $token
```
Then you will have access to the image built by CI in this repo.
```shell
docker pull ghcr.io/voltpost/everest-devcontainer
```
You should now be able to use this container in VSCode or with the [devcontainer cli](https://github.com/devcontainers/cli).
```shell
devcontainer up --workspace-folder .
devcontainer exec --workspace-folder . bash
```
