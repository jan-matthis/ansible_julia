# Julia

Ansible role to install [Julia](https://julialang.org) binaries.


## Requirements

Linux x86 64-bit system


## Installation

```commandline
$ ansible-galaxy install jan_matthis.julia
```

## Variables

```yaml
# Version
# Current stable release: https://julialang.org/downloads/#current_stable_release
julia_version:
  major: 1
  minor: 4
  build: 2

# Tarball
julia_tarball: julia-{{ julia_version.major }}.{{ julia_version.minor }}.{{ julia_version.build }}-linux-x86_64.tar.gz

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

# Mirror
julia_mirror: "https://julialang-s3.julialang.org"

# URL for downloading tarball
julia_download_url: "{{ julia_mirror }}/bin/linux/x64/{{julia_version.major}}.{{julia_version.minor}}/{{julia_tarball}}"

# Temporary directory for storing and unpacking tarball
julia_download_dir: "/tmp"

# Timeout for download
julia_download_timeout: 600
```


## Example

```yaml
- hosts: servers
  include_role:
    name: jan_matthis.julia
  vars:
    julia_dir: "{{ ansible_env.HOME }}/julia"
    julia_symlink: false
    julia_path_append: true
```


## Testing

Tests can be run using [`molecule`](https://molecule.readthedocs.io/en/latest/) and `docker`.


## License

MIT
