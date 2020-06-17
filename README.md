# Julia

Ansible role that installs [Julia](https://julialang.org) binaries for Linux x86 64-bit systems.


## Requirements

Linux x86 64-bit system


## Installation

```commandline
$ ansible-galaxy install jan-matthis.julia
```

## Role Variables

```yaml
# Version
# Current stable release: https://julialang.org/downloads/#current_stable_release
julia_version:
  major: 1
  minor: 4
  build: 2

# Checksums
# Obtainable via: https://julialang-s3.julialang.org/bin/checksums/julia-X.X.X.md5
julia_tarball_checksums:
  julia-1.4.2-linux-x86_64.tar.gz: "md5:f47a3782dc507740b299babfe989bbc7"

# Installation directory
julia_dir: "/opt/julia"

# Symlink
julia_symlink: true
julia_symlink_dir: "/usr/local"

# Append to PATH
julia_path_append: false
julia_path_append_file: "{{ansible_env.HOME}}/.profile"

# Temporary directory for storing and unpacking tarball
julia_dir_download: "/tmp"

# Mirror
julia_mirror: "https://julialang-s3.julialang.org"

# Timeout for download
julia_tarball_download_timeout: 600
```


## Example Playbook

Installation on a server without administrator rights:

```yaml
- hosts: servers
  include_role:
    name: jan-matthis.julia
  vars:
    julia_dir: "{{ ansible_env.HOME }}/julia"
    julia_symlink: false
    julia_path_append: true
```


## Testing

Tests can be run using `molecule` and `docker`, see [https://molecule.readthedocs.io].


## License

MIT
