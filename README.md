# adios-container

Attempt to build a singularity environment for ADIOS2 and MGARD.

This follows the original containers and builds the ADIOS2 environment
using Spack. Casacore and the Python bindings are then built from
source. There is a slight bodge in python-casacore build to work round
what seems to be an issue with the cmake supplied by Spack.

## Building

To build:

```
singularity build --fakeroot --force adios3.sif adios3.singularity
singularity build --fakeroot --force casa.sif casa.singularity
```

## Usage

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
python /opt/software/compress_ms.py my_example.ms DATA adios.output --numpy -a 1e-2
```

You can write a column back to a MS:

```
python /opt/software/compress_ms.py my_example.ms DATA adios.output --replace -a 1e-2
```

This creates a copy of the MS with a name related to the original. It does *not* use a compressed storage manager, it's just uncompressing the mgard compressed output back into the DATA column. So we can test the effects of compression using this column, but it's not a replacement for dysco.

## Runscript

To allow one-stop (simulated) compression you can run commands in the singularity image as follows:

```
singularity run casa.sif python /opt/software/compress_ms.py my_example.ms DATA adios.output --replace -a 1e-2
```
