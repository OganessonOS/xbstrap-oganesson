# XBStrap Distro Bootstrap files for Oganesson

This repository contains the files needed to bootstrap Oganesson using [xbstrap](https://github.com/managarm/xbstrap).

# Building
Oganesson is extremly far from being absolutely anything, however, in general, the [Managarm Handbook](https://docs.managarm.org/handbook/index.html) contains instructions on how to use `xbstrap`.

There are, however, some differences between Managarm and Oganesson to consider when building the distribution and porting packages:

- Managarm actually works, and is a fundamentally different kernel, with different design ideas, concepts and goals.
  - Oganesson does not aim to become a useable OS for daily tasks, more than its a project I can use to test out operating system concepts
  - In this regard, if you want to contribute to a operating system that may eventually become useable on a daily basis (emphasis on `may`!), look into managarm instead!
- The cross-compiler is called `cross-gcc` on Oganesson and `system-gcc` on Managarm.
  - This is because Managarm builds several different GCC targets, as it uses a different target to compile the kernel and core services, compared to compiling userland applications.
- There are at present no tasks to run qemu, or any other emulator, as no image is currently being built.
- The kernel is called `tennesine-kernel`, rather than `oganesson-kernel` or `managarm-kernel`.
- The userland does not presently exist, although a placeholder libc can be built with the target `mlibc` and `mlibc-headers`.

# Contributing and porting
`bootstrap.yml` does _not_ contain any packages or sources, in order to allow an IDE to be opened in the `bootstrap.d` folder. This is done as `xbstrap` places source directories in this folder, and an IDE may attempt to index these trees, causing massive slowdowns in some cases.
Therefore, do not add any packages to `bootstrap.yml`, instead either add them to the appropriate file in the `bootstrap.d` folder, or create a new one if no file is appropriate for the package.

The contents of `bootstrap.d` are laid out as follows:
- `oganesson` contains packages criticial to an Oganesson installation, and which are not provided by external projects
- `tools` contains only tool definitions
- `packages` contains userland packages provided by other projects
  - The `.yml` files in `packages` are named after the package groups from Gentoo, although this is not always strictly followed. New packages should be placed in the appropriate file here, or a new file named after the correct package group should be created here.
  
