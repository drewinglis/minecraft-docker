# Docker containers for Minecraft

I set these up to make it easier to build [gnembon's
CarpetMod](https://github.com/gnembon/carpetmod). The Dockerfile for vanilla
Minecraft is based on [PHLAK's
docker-minecraft](https://github.com/PHLAK/docker-minecraft) project, with some
improvements (such as server jar URL lookup from human-readable version id).

I won't link to the repositories of the prebuilt images because (as I understand
it) distributing Docker images with the Minecraft jar bundled in to them is
against the EULA, but I've included cloudbuild.yaml files so that you can build
them with Google Cloud Build if you wish (or see how one might run `docker
build` locally).

Also, at some point Mojang changed the server jar downloads from
`mojang.com/HUMAN_READABLE_VERSION-server.jar` to
`mojang.com/UNREADABLE_BLOB_ID-server.jar`, so I created a script to automate
the translations (versions are sourced from
[mcversions.net](https://mcversions.net/)).

## Running the server

The only one-time setup you need to do is create a docker volume to store the world data:

    docker volume create --name minecraft-data

To run the Minecraft server:

		GCP_PROJECT_ID=your-project-id
		MC_VERSION=1.12.2
		SERVER_TYPE=vanilla # or carpet
    docker run -it -d -p 25565:25565 -v minecraft-data:/etc/minecraft --name minecraft-server gcr.io/${GCP_PROJECT_ID}/minecraft-${SERVER_TYPE}:${MC_VERSION}

## License & Copyright

Code is licensed under the [MIT license](LICENSE.md).

The [vanilla/Dockerfile](vanilla/Dockerfile) is based on
[PHLAK's](https://github.com/PHLAK/docker-minecraft/blob/0aa21680d4284ecc290d39a74af7b1e07a95a381/Dockerfile).
See [his
license](https://github.com/PHLAK/docker-minecraft/blob/df364938c0c7c1cb2d64c782f36f3472092839b5/LICENSE)
for usage info.
