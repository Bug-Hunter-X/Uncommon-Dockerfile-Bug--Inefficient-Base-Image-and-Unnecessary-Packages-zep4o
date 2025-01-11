# Uncommon Dockerfile Bug: Inefficient Base Image and Unnecessary Packages

This repository demonstrates a common but subtle issue in Dockerfiles: using an overly large base image and installing unnecessary packages. It also shows how to use ENTRYPOINT for increased robustness. 

## Bug

The original `Dockerfile` uses `ubuntu:latest` as the base image.  `ubuntu:latest` is a very large image, resulting in larger build times and image sizes.  It also installs a lot of unnecessary packages using `apt-get`.  The `CMD` is also not robust; it does not handle cases where the user wants to pass additional arguments to the Python script.

## Solution

The `Dockerfile_fixed` demonstrates a much more optimized Dockerfile.  It uses a smaller, slimmer base image (`python:3.9-slim-buster`), installs only required packages, and uses `ENTRYPOINT` for increased robustness, allowing the user to pass arguments to the script.

## How to Reproduce

1. Clone this repository.
2. Build the original Dockerfile using `docker build -t buggy-app .`
3. Build the corrected Dockerfile using `docker build -t fixed-app -f Dockerfile_fixed .`
4. Compare the image sizes and build times.