# MonorepoNx

This is an example monorepo project that shows how to use [Nx](https://nx.dev) in conjunction with Docker & Github actions.
When a change is commited to master, Nx figures out the dependencies and lints, tests en build only the **affected** apps.
I created custom builder to create the Docker image & push it to the registry (it actually doesn't push the images to the registry, instead it just echo the command).
Also I created a custom Nx command that **tags** all **unaffected** images (based on the former COMMIT_SHA) with the new GIT_COMMIT_SHA.
In this way all COMMIT_SHA's on master will have an appropriate TAG for **all** apps, even without building them.

I also supplied a [docker-compose](docker-compose.yml) file, for you to run it locally, just do:
```bash
docker-compose up --build
```

This also showcases the use of [Traefik](https://docs.traefik.io) as proxy/ingress for docker-compose.

