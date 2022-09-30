# Deploy Jenkins continuous integration server

## Overall process

1. Jenkins builds jars based on build parameters ——> Jenkins pulls code from github ——> 
Maven into a jar package ——> Copy the jar to the specified directory according to the build parameters

2. Mirror build based on build parameters on Jenkins ——> Jenkins packages images according to Dockerfile ——> 
Push to Harbor, an enterprise-level private repository ——> Delete locally generated images

