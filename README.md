# OBSOLETE and DISABLED

As of 2022-04-05, mdi-singularity-base is disabled and not used by the MDI.
It proved difficult to maintain consistency in R package compilation due to lib stddef.h.
As the gain was incremental, preference was given to promoting the use of multiple
CPUs for apps server installation via consistent availability of option --n-cpu
in shell commands and batch scripts.

Since the main purpose of this repository was to create a container
with the R and R packages installed, it no longer has any utility.
Developers should simply use a standard OS image when
creating containers for Stage 1 pipelines, which is still recommended.

---

# MDI Singularity Base

The [Michigan Data Interface](https://midataint.github.io/) (MDI) 
is a framework for developing, installing and running 
Stage 1 HPC **pipelines** and Stage 2 interactive web applications 
(i.e., **apps**) in a standardized design interface.

This is an empty tool suite used by MDI project maintainers 
to create base Singularity container images with R Shiny installed.
It was launched using the MDI suite template:

- <https://github.com/MiDataInt/mdi-suite-template.git>

and modified via __config.yml_ and _singularity.def_
to add support for suite-level containers offering both pipelines and apps.
The consequence is that:

```bash
mdi build --suite MiDataInt/mdi-singularity-base
```

will create a container image with a base R installation with full Shiny support. 
The image also has conda installed and ready to create pipeline-specific 
environments if requested by downstream suite-level containers that list
mdi-singularity-base as their 'From' image in singularity.def.

Those resulting base image is pushed
to the MiDataInt GitHub Container Registry where it can be automatically pulled
and used by MDI install actions on a system where Singularity is available.
Installation is much faster in this scenario.

## Versioning scheme

### R-based major.minor version

MDI base container image versions correspond to
the a major.minor release of R, e.g., 4.1. This is achieved
by adding matching release tags to this repository on GitHub.

### Independent patch version

If something in this repository needs to change while maintaining the same R version,
the patch number on the tag can be incremented. Thus, it is important to remember that
the patch version of this repository is **not** the same as the patch version of R.

Together, this repository is tagged in a typical fashion as 
'**major**.**minor**.patch', 
where the bolded components correspond to the R version set in _singularity.def_.

## Using mdi-singularity-base images

MDI base images are used in two ways.  First, they can be set by a developer 
as the base image for a suite-level container as follows:

```bash
# SUITE_NAME/singularity.def
Bootstrap: oras
From: ghcr.io/MiDataInt/mdi-singularity-base:v4.1
Stage: build
```

Alternatively, they can be requested by any user during the MDI
install process on a system with Singularity installed, by simply
providing the requested major.minor R version - the installer 
pulls and uses the appropriate base image, if available.
