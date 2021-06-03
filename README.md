# Jenkins

Docker Hub can automatically build images from source code in an external repository and automatically push the built image to your Docker repositories.

When you set up automated builds, you create a list of branches and tags that you want to build into Docker images. 
When you push code to a source code branch(GitHhub) for one of those listed image tags, the push uses a webhook to trigger a new build, which produces a Docker image. The built image is then pushed to the Docker Hub registry.

If you have automated tests configured, these run after building but before pushing to the registry. 
You can use these tests to create a continuous integration workflow where a build that fails its tests does not push the built image. 
Automated tests do not push images to the registry on their own.
