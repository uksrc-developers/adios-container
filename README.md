# adios-container

Attempt to build a singularity environment for ADIOS2 and MGARD.

To build:

```
singularity build --fakeroot --force adios.sif adios.singularity
singularity build --fakeroot --force casa.sif casa.singularity
```

To run a shell in the casa container

```
singularity shell casa.sif
```
