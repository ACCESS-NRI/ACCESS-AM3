![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2FACCESS-AM3%2Fraw%2Fmain%2Fconfig%2Fversions.json&query=%24.spack-packages&label=ACCESS-NRI%2Fspack-packages) ![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2FACCESS-AM3%2Fraw%2Fmain%2Fconfig%2Fversions.json&query=%24.spack&label=ACCESS-NRI%2Fspack) ![Dynamic JSON Badge](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fgithub.com%2FACCESS-NRI%2Fbuild-cd%2Fraw%2FHEAD%2Fconfig%2Fsettings.json&query=%24.deployment.Gadi.Release.%5B'0.22'%5D.spack-config&label=ACCESS-NRI%2Fspack-config%20(Gadi))

# ACCESS-AM3

## About the model
The ACCESS-AM model is an atmosphere-land climate model for the biogeophysics and biogeochemistry. ACCESS-AM3 forms part of the ACCESS-ESM3 Earth system model.

## Support

Any questions about ACCESS-NRI releases of ACCESS-AM3 should be done through the [ACCESS-Hive Forum](https://forum.access-hive.org.au/). See the [ACCESS Help and Support topic](https://forum.access-hive.org.au/t/access-help-and-support/908) for details on how to do this.

### Build

ACCESS-NRI is using [spack](https://spack.io), a build from source package manager designed for use with high performance computing. This repository contains a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) definition file ([`spack.yaml`](https://github.com/ACCESS-NRI/ACCESS-AM3/blob/main/spack.yaml)) that defines all the essential components of the ACCESS-AM3 model, including exact versions.

Spack automatically builds all the components and their dependencies, producing model component executables. Spack already contains support for compiling thousands of common software packages. Spack packages for the components in ACCESS-AM3 are defined in the [spack packages repository](https://github.com/ACCESS-NRI/spack_packages/).

ACCESS-AM3 is built and deployed automatically to `gadi` on NCI (see below). However it is possible to use spack to compile the model using the `spack.yaml` environment file in this repository. To do so follow the [instructions on the ACCESS-Hive Forum for modifying and building an ACCESS model's source code](https://docs.access-hive.org.au/models/run-a-model/build_a_model/).

Then clone this repository and run the following commands on `gadi`:

```bash
spack env create access-am3 spack.yaml
spack env activate -p access-am3
spack install
```

to create a spack environment called `access-am3` and build all the ACCESS-AM3 components, the locations of which can be found using `spack find --paths`.

### Deployment

ACCESS-AM3 is deployed automatically when a new version of the [`spack.yaml`](https://github.com/ACCESS-NRI/ACCESS-AM3/blob/main/spack.yaml) file is committed to `main` or a dedicated `backport/VERSION` branch. All the ACCESS-AM3 components are built using `spack` on `gadi` and installed under the [`vk83`](https://my.nci.org.au/mancini/project/vk83) project in `/g/data/vk83`. It is necessary to be a member of [`vk83`](https://my.nci.org.au/mancini/project/vk83/join) project to use ACCESS-NRI deployments of ACCESS-AM3.

The deployment process also creates a GitHub release with the same tag. All releases are available under the [Releases page](https://github.com/ACCESS-NRI/ACCESS-AM3/releases). Each release has a changelog and meta-data with detailed information about the build and deployment, including:

- paths on `gadi` to all executables built in the deployment process (`spack.location`)
- a `spack.lock` file, which is a complete build provenance document, listing all the components that were built and their dependencies, versions, compiler version, build flags and build architecture
- the environment `spack.yaml` file used for deployment

Additionally the deployment creates environment modulefiles, the [standard method for deploying software on `gadi`](https://opus.nci.org.au/display/Help/Environment+Modules). To view available ACCESS-AM3 versions on `gadi`:

```bash
module use /g/data/vk83/modules
module avail access-am3
```

For users of ACCESS-AM3 model configurations released by ACCESS-NRI, the exact location of the ACCESS-AM3 model executables is not required. Model configurations will be updated with new model components when necessary.
