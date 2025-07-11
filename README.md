# Repo manifest for OP-TEE integrated with liboqs for post-quantum  fTPM

## Build instruciton
```text
$ mkdir optee
$ cd optee
$ repo init -u https://github.com/torsec/manifest.git
$ repo sync
$ cd build
$ make toolchains
$ export PATH="$PATH:<project-dir-path>/toolchains/aarch32/bin"
```

## Change ```tpm2-tools``` and ```tpm2-tss``` sources

### tpm2-tools
In the ```<project-dir-path>/buildroot/package/tpm2-tools/tpm2-tools.mk``` comment the line:

```
TPM2_TOOLS_SITE = https://github.com/tpm2-software/tpm2-tools/releases/download/$(TPM2_TOOLS_VERSION)
```

and add the two following lines:

```
TPM2_TOOLS_SITE_METHOD = local
TPM2_TOOLS_SITE = <project-dir-path>/build/../tpm2-tools-5.7.2
```


### tpm2-tss
In the ```<project-dir-path>/buildroot/package/tpm2-tss/tpm2-tss.mk``` comment the line:

```
TPM2_TSS_SITE = https://github.com/tpm2-software/tpm2-tss/releases/download/$(TPM2_TSS_VERSION)
```

and add the two following lines:

```
TPM2_TSS_SITE_METHOD = local
TPM2_TSS_SITE = <project-dir-path>/build/../tpm2-tss-3.2.2.1
```

### rust-keylime

Move in the ```<project-dir-path>/rust-keylime``` directory and run:

```
$ cargo fetch
```

In the ```<project-dir-path>/build/br-ext/package/rust_keylime_ext/rust_keylime_ext.mk``` change the variable ```RUST_KEYLIME_EXT_CARGO_ENV``` in:

```
RUST_KEYLIME_EXT_CARGO_ENV = \
     CARGO_HOME=<user_home>/.cargo
```

In addition, in the same file change the ```RUST_KEYLIME_EXT_SITE``` variable in:

```
RUST_KEYLIME_EXT_SITE = <project-dir-path>/rust-keylime
```

Finally set the supported Rust version:

```
$ rustup default 1.72.0
```

or if the cargo home is different fro the user home, put the correct path.

## Build
```
$ cd <project-dir-path>/build
$ make MEASURED_BOOT_FTPM=y run
```

## Modified components
- PQ fTPM (https://github.com/torsec/ms-tpm-20-ref/tree/pq-ftpm)
- fTPM OP-TEE TA (https://github.com/torsec/optee_ftpm)
- liboqs (https://github.com/torsec/liboqs)
- TPM 2.0 TSS (https://github.com/torsec/tpm2-tss)
- tpm2-tools (https://github.com/torsec/tpm2-tools)
- linux (https://github.com/torsec/linux)
- rust-keylime (https://github.com/torsec/rust-keylime)
- buildroot (https://github.com/torsec/buildroot)

# Offical OP-TEE Implementation
## Repo manifest for OP-TEE development
This git contains repo manifests to be able to clone all source code needed to
be able to setup a full OP-TEE developer build.

All official OP-TEE documentation has moved to http://optee.readthedocs.io. The
information that used to be here in this git can be found under [manifests].

// OP-TEE core maintainers

[manifests]: https://optee.readthedocs.io/en/latest/building/gits/build.html#manifests
