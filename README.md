# adios-container

Attempt to build a singularity environment for ADIOS2 and MGARD.

This follows the original containers and builds the ADIOS2 environment
using Spack. Casacore and the python bindings are then built from
source.

To build:

```
singularity build --fakeroot --force adios3.sif adios3.singularity
singularity build --fakeroot --force casa.sif casa.singularity
```

To run a shell in the casa container

```
singularity shell casa.sif
```

Testing compression:
```
. /entrypoint.sh
python /opt/software/compress_ms.py my_example.ms DATA adios.output -a 1e-2
```

This will put the DATA column in adios.output. Note that if accuracy
is too small you will get an error message.

You can uncompress to a numpy file:

```
. /entrypoint.sh
python /opt/software/compress_ms.py my_example.ms DATA adios.output --numpy -a 1e-2
```

