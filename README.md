# Repo manifest for OP-TEE integrated with liboqs for post-quantum  fTPM

## Build instruciton
```text
$ mkdir optee
$ cd optee
$ repo init -u https://github.com/torsec/manifest.git
$ repo sync
$ cd build
$ make toolchains
$ make run
```

## Modified components
- PQ fTPM (https://github.com/torsec/ms-tpm-20-ref/tree/pq-ftpm)
- fTPM OP-TEE TA (https://github.com/torsec/optee_ftpm)
- liboqs (https://github.com/torsec/liboqs)
- TPM 2.0 TSS (https://github.com/torsec/tpm2-tss)
- tpm2-tools (https://github.com/torsec/tpm2-tools)

# Offical OP-TEE Implementation
## Repo manifest for OP-TEE development
This git contains repo manifests to be able to clone all source code needed to
be able to setup a full OP-TEE developer build.

All official OP-TEE documentation has moved to http://optee.readthedocs.io. The
information that used to be here in this git can be found under [manifests].

// OP-TEE core maintainers

[manifests]: https://optee.readthedocs.io/en/latest/building/gits/build.html#manifests
