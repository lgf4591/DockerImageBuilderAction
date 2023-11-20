# DockerImageBuilderAction
dockerhub-image-builder

- [Push Docker Images to GitHub Container Registry](https://www.youtube.com/watch?v=RgZyX-e6W9E)

# 如何使用

```yaml

name: Use the Composite Action with Actions

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Do anything elsee
        run: echo Pretend to do other things 

      # Uses the Composite Action
      - name: Build and Push the image to DockerHub
        uses: lgf4591/DockerImageBuilderAction@main
        with:
          registry_username: ${{secrets.DOCKERHUB_USERNAME}}
          registry_password: ${{secrets.DOCKERHUB_PASSWORD}}
          image_name: alpine
          tag: $GITHUB_RUN_NUMBER
          build_context: .
      
      - name: Build and Push the image to Github Packages
        uses: lgf4591/DockerImageBuilderAction@main
        with:
          registry: ghcr.io  # 必须写， 但是dockerhub不能写
          registry_username: ${{github.repository_owner}}
          registry_password: ${{secrets.GHCR_TOKEN}}
          image_name: alpine
          tag: $GITHUB_RUN_NUMBER
          build_context: .


```