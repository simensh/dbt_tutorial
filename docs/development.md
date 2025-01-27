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
git clone git@github.com:simensh/dbt_tutorial.git
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
pip install python3 -m pip install -r requirements.txt
```

### Set up connection and ensure your profile is setup correctly from the command line

In order to test local changes by deploying dbt models to DuckD, you will need to set up a connection first.
Create [profiles.yml](https://docs.getdbt.com/docs/core/connect-data-platform/profiles.yml) in `dbt_tutorial` folder
or in your user's home folder `~/.dbt/`.

```bash
dbt --version
dbt debug
```



## SQL linting

We use [sqlfluff](https://docs.sqlfluff.com) for linting the SQL code / dbt models.  
All sqlfluff configs are done in the [pyproject.toml](../pyproject.toml) file.


### Linting during development
#### IDE / code editor
Some IDEs has sqlfluff-extensions which gives you inline linting while you're coding. It's highly recommended to get this, as it increases productivity and makes it easier to learn how we format our sql code.
 - [URL](https://marketplace.visualstudio.com/items?itemName=dorzey.vscode-sqlfluff) to VSCode exstension.
 - [URL](https://plugins.jetbrains.com/plugin/20494-sqlfluff-linter-community-edition-) to IntelliJ IDEA plugin.  

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


### Linting pre-commit

The pre-commit hook you installed in the previous step ([.pre-commit-config.yaml](../.pre-commit-config.yaml)) will make
sure that `sqlfluff` is run before each `git commit`. In case of linting errors, your commit will be declined, and you
must fix linting errors before continuing.

If you want to skip the pre-commit hook validation (not recommended), you can do the following:

_Windows_

```bash
$env:SKIP='sqlfluff-lint'; git commit -m "your commit message"
```

_Mac and Linux_

```bash
SKIP=sqlfluff-lint git commit -m "your commit message"
```

### Linting in CI pipeline for merge requests

SQL linting is run by CI pipelines for branches in merge requests. The linting errors are meant to be informational and
will not stop approval and merge for changes to the `main` branch.

## CI/CD

The CI/CD pipeline for dbt is set up using a solution described by dbt Labs. The [CI pipeline](https://docs.getdbt.com/docs/deploy/continuous-integration) utilizes the webhook functionality in Gitlab and triggers automatically a CI job in dbt Cloud. This is an out of the box solution supported by dbt Cloud. The drawback is that the pipeline can only run in one environment and there are limitations to custimisation. The [CD job](https://docs.getdbt.com/guides/custom-cicd-pipelines) is set up using gitlab CI and a python script that triggers a job in dbt Cloud. This offers great custimisation options, but it also means that we manage the pipeline ourselves. (This script could be used to set up a CI pipeline as well, but it requires that a script to clean up development schemas in Snowflake has been developed first.)

References:
- https://docs.getdbt.com/guides/custom-cicd-pipelines
- https://www.getdbt.com/blog/adopting-ci-cd-with-dbt-cloud
- https://towardsdatascience.com/running-dbt-using-gitlab-ci-cd-8a2ef0f05af0