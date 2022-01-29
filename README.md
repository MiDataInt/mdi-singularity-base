# mdi-singularity-base

This is an empty tool suite used by MDI project maintainers 
to create base Singularity container images with R Shiny installed.
It was launched using the MDI suite template:

- <https://github.com/MiDataInt/mdi-suite-template.git>

and modified via '_config.yml' and 'singularity.def'
to add support for suite-level containers offering both pipelines and apps.


The consequence is that:

```bash
mdi build MiDataInt/mdi-singularity-base
```

will create a container image
with a base R installation with full Shiny support. Those images are pushed
to the MiDataInt GitHub Container Registry where they are automatically pulled
and used by MDI install and run actions on a system where Singularity is available.
Installation is much faster in this scenario.

## Versioning scheme

### R-based major.minor version

MDI base container image versions correspond to
the a major.minor release of R, e.g., 4.1. This is achieved
by adding matching release tags to this repository on GitHub.

### Independent patch version

If something in this repository needs to change while maintaining the same R version,
the patch number on the tag can be incremented. Thus, it is important to remember that
the patch version of this repostiory is **not** the same as the patch verion of R.

Together, this repository is tagged in a typical fashion as 
'**major**.**minor**.patch', 
where the bolded components correspond to the R version set in 'singularity.def'.
