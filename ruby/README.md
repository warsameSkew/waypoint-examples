# Getting Started with Waypoint and Ruby

## What will we accomplish?

In this getting started guide we will go through using Waypoint to deploy a Ruby application on Docker for Destkop. We will demonstrate this using the `pack` build for Waypoint which uses the Cloud Native Buildpacks to automatically detect application language and run your app without the need of a Dockerfile.

This repo uses a basic Ruby based application. All files you need for the application side are kept within this repository.

## Requirements

This walkthrough assumes the following...

- You have cloned this `Waypoint Examples` repository
- You have obtained the `Waypoint` binary
- You have access to the Waypoint server image in the GitHub docker image repository
- You have installed [Docker for Desktop](https://www.docker.com/products/docker-desktop)

## First Steps

### Installing the Waypoint server

We will start by installing the Waypoint server on Docker for Desktop. This installation is done by executing the following command locally on your workstation:

```bash
waypoint install --platform=docker
```

In a few moments you should receive a message that the configuration was successful. We're now ready to get started with deploying the application

### "waypoint init" - Configuring your repository

Assuming you are in the directory for this project, we can leverage the `waypoint.hcl` file contained in this sample directory to get started. In projects where no `waypoint.hcl` file exists, this can be created by executing the `waypoint init` command which will generate a basic `waypoint.hcl` file that you can customize. In the case of the example already in this directory, it is configured with sane defaults.

With the file in place, execute the following command to initialize your project and the application

```bash
waypoint init
```

### "waypoint up" - Deploying the application

This application is configured to use Cloud Native Buildpacks to detect the type of application running and launch it within Docker. This configuration means that the user doesn't need to build a Dockerfile manually, but also accepts the default configurations that the Cloud Native Buildpack leverages. It also uses the local Docker instance to build and store the image. For advanced use cases, see the `registry` stanza which allows you to automatically push your built artifact to a registry. We can deploy our application onto docker with the following command:

```bash
waypoint up
```

You should be able to observe waypoint run through the build and deploy process, and ultimately return you URL from Horizon. The response should look something like the below...

```
The deploy was successful! A Waypoint deployment URL is shown below. This
can be used internally to check your deployment and is not meant for external
traffic. You can manage this hostname using "waypoint hostname."

           URL: https://instantly-worthy-shrew.alpha.waypoint.run
Deployment URL: https://instantly-worthy-shrew--01EJ0F2VYWTNTYJ6FNFNTY44G9.alpha.waypoint.run
```

### "waypoint up" part 2 - Editing your application and iterating

One of the most powerful parts of Waypoint is the ability to iterate on deployments and quickly redeploy the application with your changes in place. Lets edit our application and show off how Waypoint can manage the lifecycle of a new deployment.

Using your favorite IDE, edit the following file `app/views/welcome/index.erb`.

- On line 8 - Edit this line to include a catchy phrase. I prefer a quote from your favorite Marvel Cinematic Universe movie, but hey, live your dream. This is about you as the application developer!

Save your file, and re-run the `waypoint up` command

Upon completion, you'll note that you're provided the same URL as above. The Waypoint server has handled automatically swithching the URL to use the most recent version of your deployment. You can access this URL and see the new version of your application!
