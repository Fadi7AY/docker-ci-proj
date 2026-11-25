# Flask · Docker CI

A containerized Flask application with a GitHub Actions image-publishing workflow.


```mermaid
flowchart LR
    N0["Push to main"]
    N1["Docker build"]
    N2["Docker Hub login"]
    N3["Publish docker-ci-project:latest"]
    N0 --> N1 --> N2 --> N3
```


## Run locally

```bash
docker build -t docker-ci-project .
docker run --rm -p 5000:5000 docker-ci-project
```

The Dockerfile exposes port 5000 and runs `app/app.py`.

## CI configuration

The workflow uses repository secrets `DOCKER_USERNAME` and `DOCKER_PASSWORD` to publish
`<DOCKER_USERNAME>/docker-ci-project:latest` after a push to `main`.

| File | Purpose |
| --- | --- |
| [Dockerfile](Dockerfile) | Python 3.12 image with Flask. |
| [app](app) | Application source. |
| [.github/workflows/docker-build.yml](.github/workflows/docker-build.yml) | Docker Hub publishing workflow. |
