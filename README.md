# Alora

This is an implementation of the Alora protocol


## Running pre-built binaries
### Release Dependencies
To run a working Anoma Node the following dependencies are required:

1. Mac OS X Development Environment:
    * Install Apple Command Line Developer Tools: `xcode-select --install`
    * Install [MacPorts](https://www.macports.org/install.php) (or equivalent package manager)
2. Install [ncurses](https://ports.macports.org/port/ncurses/) (Mac OS X only)
3. Install OpenSSL:
    * Mac OS X and Linux: use package manager
    * Windows: not required
### Running
Download the [Alora release]([https://github.com/anoma/anoma/releases](https://github.com/Aloraio/Alora)) for your platform, extract it, and run `bin/anoma`.
## Compilation from sources
### Build Dependencies

Dependencies needed regardless of platform.
 - Elixir: consult the installation instructions [here]()
 - Rust: consult the installation instructions [here](https://www.rust-lang.org/tools/install).
 - Protobuf: consult the installation instructions [here](https://grpc.io/docs/protoc-installation/)
 - Elixir plugin for protobufs `protoc-gen-elixir`
   ```shell
   mix escript.install hex protobuf 0.11.0
   ```

----
#### MacOS
Ensure Apple Command Line Developer Tools are installed.

```shell
xcode-select --install
```

Using `brew`, install the following dependencies.

```shell
brew install elixir cmake protobuf git
```

---
#### Ubuntu/Debian

Dependencies that you might not have installed.

```shell
apt install cmake
```

---
#### Windows

 - Install [Build Tools for Visual Studio 2022](https://visualstudio.microsoft.com/downloads/) (Workload: Visual C++ build tools)
 - Install [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4)


---
### Compiling and Running

To install the dependencies as well as Alora run:

```bash
mix deps.get
mix compile
```

To start an Alora instance run one of these:

```bash
iex -S mix # starts an interactive shell
mix run --no-halt # starts a non-interactive shell
```

See the Contributing section for how to get the best use of the
interactive shell.

Further see the Known issues section if you encounter an issue.


## Docker images
To work with Docker images, do the following:
1. Install [Docker](https://docs.docker.com/engine/install/), this is necessary for both building and running Docker images
2. Build the Alora image from the repository root: `docker build -t <IMAGE> .`
    * `<IMAGE>` is your chosen image name
4. Run the Alora image: `docker run -it --network host <IMAGE> <SUBCOMMAND>`
    * `<IMAGE>` is the name of Anoma Docker image to be run
    * `<SUBCOMMAND>`is interpreted by the Anoma binary
    * `--network host` will enable connections from the host

## Contributing

Please read the [contributor's guide](./documentation/contributing.livemd) for in
depth details about the codebase.

## Known Issues

### (Mix) Could not compile dependency :enacl

For some versions of OSX (and Linux), our
[enacl](https://github.com/jlouis/enacl) package may have compilation issues.

To get around it please run

```sh
git checkout mariari/no-libsodium
mix clean
mix deps.get
mix compile
```

### could not compile dependency :cairo, "mix compile"

The rust compiler can be quite picky about our
[cairo](https://github.com/anoma/aarm-cairo) dependencies. This is
likely caused by an incompatible rust-toolchain.

To get around it you may have to run a command like:

```sh
rustup toolchain add 1.76.0
# for OSX you may try 1.76.0-aarch64-apple-darwin
```

Once this is had, the Cairo issues should go away.

### Git

This codebase follows a git style similar to
[git](https://git-scm.com/) or
[linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git).

New code should be based on `base`, and no attempt to keep it up to
sync with `main` should be had. When one's topic is ready, just submit
a PR on github and a maintainer will handle any merge conflicts.

There are bi-weekly releases, so do not be afraid if a maintainer says
the PR is merged but it's still open, this just means that it's merged
into `next` or `main` and will be included in the next scheduled
release.

For more information on a smooth git experience check out the [git
section in contributor's guide](./documentation/contributing/git.livemd)

Happy hacking, and don't be afraid to submit patches.
