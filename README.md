# Docker LAMP Test Bed

I found a great Docker Hub image at `greyltc/lamp` - but I needed a few changes for
my development setup.  I use this for development, experimentations or demonstrations.
Do not use this image for a production-based system as I've configured it.

## Changes from Original Image

- document root is now `/srv/http/public`, but you should still mount at `/srv/http`. This allows you to have PHP code outside of doc root.
- display errors is turned on for PHP

## Recommended Docker Run Command

`docker run --name lamp-testbed -p 9080:80 -p 9443:443 -v ~/your-project:/srv/http aaronsaray/lamp-testbed`

This does the following:

- pulls the container `aaronsaray/lamp-testbed`
- names the container `lamp-testbed`
- forwards all requests on `http://localhost:9080` to the container's apache
- forwards all requests on `https://localhost:9443` to the container's SSL apache instance
- mounts the files from your directory `~/your-project` to `/srv/http` in the machine (remember, it's `public` as a doc root, so your local code must have that, too)

You can view https://hub.docker.com/r/greyltc/lamp/ for great instructions on
his original image.

## Further Considerations

Again, I can't stress this enough - **this should only be for quick experimentation**.
Even for local development, using something like this can be bad.  Your production
systems may not ever have a local MySQL for example - plus this concept defies
Docker's single-container single-concern type of model.  So, once you've proved your
point with this throw-away docker image, please use individual ones for PHP + MySQL.
