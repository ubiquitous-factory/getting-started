# getting-started
A template for the [getting started](https://ubifac.tech/howto/getting-started) documentation

See https://ubifac.tech/howto/getting-started for detailed instructions on how to use this.


For those just looking for a reminder of the steps: 

1. Make sure you have [podman](https://podman.io/docs/installation) and [podman-bootc](https://github.com/containers/podman-bootc) installed

1. Use the `Use this template button` at the top right of the screen to create a copy of the project.

1. Edit find the `Environment=ENDPOINT=` in the `brog.service` file and set value to be the location of the  brog.yaml file in your new repo
   e.g. 
   ```bash
   Environment=ENDPOINT=https://raw.githubusercontent.com/octocat/open-coras/refs/heads/main/brog.service
   ```

1. In `.github.workflows/build-push.yaml` change the `IMAGE_NAME:` variable to the name of the project
   e.g.
   ```yaml
    IMAGE: getting-started
   ``` 


1. In `.github.workflows/build-push.yaml` change the `REGISTRY:` variable to the name of the ghcr.io/OWNERNAME
   e.g.
   ```yaml
    REGISTRY: ghcr.io/octocat
   ``` 

1. Commit the changes to the project

1. The build should take ~5 mins to run and will generate a package in the repository

1. Make the [package public](https://docs.github.com/en/packages/learn-github-packages/configuring-a-packages-access-control-and-visibility) 

1. Run the image 
   e.g. 
   ```bash
   podman-bootc run --filesystem xfs ghcr.io/octocat/getting-started:5dd152682b3cd3bb24ecc2947d78a6ac94e2c9f6
   ```

1. Add the following line to the `Containerfile`
   ```dockerfile
   COPY LICENCE /etc
   ```
1. Commit the changes to the project

1. The build should take ~5 mins to run and will generate a package in the repository

1. Now edit the brog.yaml to match the new build image definition that contains the `LICENCE` file. It will be the top option in the package screen.
   e.g. 
   ```yaml
   clientConfig:
      image: ghcr.io/octocat/getting-started:34sdfsdf682b3cd3bb24ecc2947d78a6ac94e2c9f6
   ``` 

1. The running VM will now terminate 

1. Run the image again with `podman-bootc`  
   ```bash
   # get the list of images
   podman-bootc list
   # run the image using the id
   podman-bootc run IDOFIMAGE
   ```

1. Validate the `LICENCE` file is present 
   ```bash
   cat /etc/LICENCE
   ```

Well done you've successfully used GitOps with bootc. 
