# Explore buildpacks.io

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Pre-requisites:
* Install docker
* Start Docker daemon
* Intall buildpack: https://buildpacks.io/docs/tools/pack/ 
* (optional) Set default buildpack
pack config default-builder <bp-id>

## Test buildpacks lyfecycle

Following this [buildpack doc: Create a buildpack]( https://buildpacks.io/docs/buildpack-author-guide/create-buildpack/building-blocks-cnb/) with a [CRA app](https://create-react-app.dev/)


1/ Create buildpack 
```
pack buildpack new examples/node-js \
    --api 0.8 \
    --path node-js-buildpack \
    --version 0.0.1 \
    --stacks io.buildpacks.samples.stacks.jammy
```    
In `./node-js-buildpack` there is a skeleton for template builpack.
Here you can hook on lifecycle: detect, build

2/ Write code to override build phase
I cutomized the `./node-js-buildpack/bin/detect` and `./node-js-buildpack/bin/build` in my custom buildpack to use a psecific version of node as per tutorial.

3/ Build with custom buildpack
```
pack build my-app3 --buildpack ./node-js-buildpack
docker run --platform linux/amd64 -p 3000:3000 my-app3
```
Note: when working on macOS to remove warning use  `--platform linux/amd64` see [here](https://medium.com/@email.bajaj/docker-image-platform-compatibility-issue-with-mac-silicon-processors-m1-m2-ee2d5ea3ff0e 
)

In you browser go to `http://localhost:3000`

