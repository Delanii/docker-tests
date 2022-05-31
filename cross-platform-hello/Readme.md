# How this image was built

1. Install `docker`, depending on your platform.
2. Inspect defined builders with `docker buildx ls`. If you do this for the first time, it should be the `default` builder.
3. Create a new docker builder with:

   ```bash
  docker buildx create --name my-new-builder --platform $(platform-list)
   ```

   I wasn't able to find a complete reference to all values supported for `$(platform-list)` variable, but I use these:
   

    ```bash
  docker buildx create --name my-new-builder --platform linux/amd64,linux/arm64,windows/amd64,macos/arm64,macos/amd64
   ```

4. Set the new builder as the default builder:

   ```bash
   docker buildx use my-new-builder
   ```
   
5. Inspect your new default builder with `docker buildx inspect`
6. Bootstrap your builder with `docker buildx inspect --bootstrap`
7. Login to DockerHub with `docker login`
8. Build the image and push it to the docker hub with

   ```bash
   docker buildx build --platform linux/amd64,linux/arm64,windows/amd64,macos/arm64,macos/amd64 -t delanii/cross-platform-hello . --push
   ```

# How to use this image

# Tips

- command `docker buildx` prints a help overview in the terminal
<!--  LocalWords:  DockerHub
 -->
