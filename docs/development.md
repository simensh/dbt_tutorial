# Development

Below are instructions on how to set up local development environment to work with dbt models.

## Set up local development

### Recommended IDE

Recommended IDE is either [VSCode](https://code.visualstudio.com) (with
extension [dbt Power User](https://marketplace.visualstudio.com/items?itemName=innoverio.vscode-dbt-power-user)) or
[IntelliJ IDEA](https://www.jetbrains.com/idea/).

### Install Python

You need python to work with models locally. Check [dbt docs](https://docs.getdbt.com/docs/core/pip-install) for
which version python is supported.

### Clone this repo

```bash
git clone https://github.com/simensh/dbt_tutorial.git
```

### Create virtual environment in python

Create virtual development environment in python by using [venv](https://docs.python.org/3/library/venv.html).
> If you have installed multiple Python versions, make sure to switch to the correct Python version before creating the
> virtual environment.

_Windows (python v11)_

```bash
cd dbt_tutorial
py -3.11 -m venv .venv
```

_Mac and Linux_

```bash
cd dbt_tutorial
python3.11 -m venv .venv
```

### Activate virtual environment

You need to activate the virtual environment every time you open a new shell.

_Windows_

```bash
.venv\Scripts\activate
```

_Mac and Linux_

```bash
source .venv/bin/activate
```

### Install required dependencies

Update pip to latest version

```bash
python3 -m pip install --upgrade pip
```

Install packages

```bash
python3 -m pip install -r requirements.txt
```

### Set up connection and ensure your profile is setup correctly from the command line

In order to test local changes by deploying dbt models to DuckD, you will need to set up a connection first.
You can create a [profiles.yml](https://docs.getdbt.com/docs/core/connect-data-platform/profiles.yml) in `dbt_tutorial` folder
or in your user's home folder `~/.dbt/`, if you don't want to use the existing common profile.yml file.

```bash
dbt --version
dbt debug
```

## SQL linting

We use [sqlfluff](https://docs.sqlfluff.com) for linting the SQL code / dbt models.  


### Linting during development
#### IDE / code editor
Some IDEs has sqlfluff-extensions which gives you inline linting while you're coding. It's highly recommended to get this, as it increases productivity and makes it easier to learn how we format our sql code.
 - [URL](https://marketplace.visualstudio.com/items?itemName=dorzey.vscode-sqlfluff) to VSCode exstension.

After installing the extension, you need to make sure that it will use the `sqlfluff` installation in your local development environment. You do this by adding the sqlfluff executable path as a config to the extension.  

In VSCode: edit your vscode settings.json file (in .vscode folder) and add the appropriate parameter:
 - Mac and Linux: `"sqlfluff.executablePath": "${workspaceFolder}/.venv/bin/sqlfluff"`
 - Windows: `"sqlfluff.executablePath": "${workspaceFolder}/.venv/scripts/sqlfluff.exe"`

#### Command line
You can also run linting manually:

```bash
sqlfluff lint <path to sql file>
```

And/or fix linting errors automatically with:

```bash
sqlfluff fix <path to sql file>
```

> It's always advised to review the linting fixes done automatically by `sqlfluff fix`, before pushing changes remotely.
