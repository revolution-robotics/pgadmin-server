# pgAdmin Installer GNU/Linux Desktop environments

This script installs a local Flask-based **pgAdmin** server together
with **GNU/Linux** desktop suport and a systemd service. During
installation, if a *~/.pgadmin* directory does not already exist,
credentials are prompted for (and used to encrypt saved passwords) and
the **pgAdmin** (**SQLite**) database is updated accordingly.

Files installed for **GNU/Linux** desktop and systemd support include:

- [**pgAdmin**](https://www.pgadmin.org) *config_local.py* (setting, e.g.: `DATA_DIR=~/.pgadmin`),
- [**systemd**](https://systemd.io) unit file *${HOME}/.config/systemd/user/pgadmin.service*,
- [**XDG**](https://www.freedesktop.org/wiki) desktop entry *${HOME}/.local/share/applications/pgadmin.desktop*, and
- command-line script *${HOME}/bin/pgadmin-ctl*.

To start the **pgAdmin** service and open the **pgAdmin** URL (by
default: http://localhost:5050), either run in a terminal:
`pgadmin-ctl start` or click on the **pgAdmin** desktop icon. To check
the status of **pgAdmin**, in a terminal, run:

```shell
pgadmin-ctl status
```

To stop **pgAdmin**, use:

```
pgadmin-ctl stop
```

# Prerequisites

- **GNU** `autoconf`
- **GNU** `make`
- `python3` and `pip3`
- [`jq`](https://github.com/stedolan/jq)

# Install **pgAdmin**

To install **pgadmin** in virtual environment, run:

```shell
git clone https://github.com/revolution-robotics.com/pgadmin-installer
cd ./pgadmin-installer
python -m venv ~/.local/pgadmin
source ~/.local/pgadmin/bin/activate
```

Within the virtual environment (command prompt is prefixed by *(pgadmin)*):

```shell
./autogen.sh
./configure --with-opt-path=${HOME}/.local/pgadmin/bin
gmake install
deactivate
```

Finally, update PATH as necessary to include ~/bin:

```shell
export PATH+=:~/bin
```

# Upgrade **pgAdmin**

The virtual environment can be upgraded as follows:

```shell
/path/to/new/python -m venv --upgrade --upgrade-deps ~/.local/pgadmin/bin
```

# Remove **pgAdmin**

After installation, to remove the **pgAdmin** service and associated
files other than *~/.pgadmin* and the virtual environemnt, run:

```shell
make -C /path/to/pgadmin-installer uninstall
```

To remove the virtual environment, use:

```shell
rm -rf ~/.local/pgadmin
```
