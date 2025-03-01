<p align="center">
  <a href="https://github.com/stonefish-dev/license-manager"><img alt="SLiM" src="https://raw.githubusercontent.com/stonefish-dev/license-manager/main/images/stonefish-license-manager-logo.svg" width="60%"></a>
</p>

[![PyPi Version](https://img.shields.io/pypi/v/stonefish-license-manager.svg?style=flat-square)](https://pypi.org/project/stonefish-license-manager/)

The Stonefish License Manager (SLiM) is a command-line tool and library that
efficiently manages the licenses for your Python software. Installation is
as simple as

```sh
pip install stonefish-license-manager
```

For detailed development information, please refer to
[README-dev.md](README-dev.md).

### Quickstart Guide for End Users

- Install or uninstall a license:

  <!--pytest.mark.skip-->

  ```sh
  slim install <license-file-or-key>
  slim uninstall <license-file-or-key-or-id>
  ```

- List all installed licenses:

  ```sh
  slim ls
  ```

  <p align="center">
    <img alt="SLiM" src="https://raw.githubusercontent.com/stonefish-dev/license-manager/main/images/termshot-slim-ls.png" width="80%">
  </p>

- (De)activate installed licenses:

  <!--pytest.mark.skip-->

  ```sh
  slim [de]activate <license-file-or-key-or-id>
  ```

  <p align="center">
    <img alt="SLiM" src="https://raw.githubusercontent.com/stonefish-dev/license-manager/main/images/termshot-slim-activate.png" width="80%">
  </p>

- Show the machine fingerprint:

  ```sh
  slim fingerprint
  ```

  ```
  5ea8aa03de6ce4398acdd2cd65f4e28af
  ```

All command line options can be accessed by running the following command:

<!--pytest.mark.skipif(sys.version_info < (3, 11), reason="-h output changes slightly")-->

```sh
slim -h
```

<!--pytest-codeblocks: expected-output-ignore-whitespace-->

```
Usage: slim [-h] [--version]
            {versions,vv,list,ls,show,info,install,add,a,uninstall,remove,rm,delete,del,activate,deactivate,fingerprint,fp,refresh,cache}
            ...

Stonefish License Manager.

Options:
  -h, --help            show this help message and exit
  --version, -v         display version information

Subcommands:
  {versions,vv,list,ls,show,info,install,add,a,uninstall,remove,rm,delete,del,activate,deactivate,fingerprint,fp,refresh,cache}
    versions (vv)       Display version information, including dependencies
    list (ls, show, info)
                        List installed licenses
    install (add, a)    Install (and activate) licenses
    uninstall (remove, rm, delete, del)
                        Uninstall (and deactivate) licenses
    activate            Activate machine for license
    deactivate          Deactivate machine for license
    fingerprint (fp)    Display machine fingerprint
    refresh             Refresh license files and cache
    cache               Manage the cache
```

### Additional Information

For further information, please contact support@mondaytech.com.
