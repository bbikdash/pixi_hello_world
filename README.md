# Experimenting with `pixi`

Tested with `pixi 0.62.1`.

Seems really fast to install packages and it seems to integrate the python environment with VS Code just fine.

Keep in mind most of the pixi management process is automated with high level commands. Adding/removing packages via the cli auto-updates the `.toml` file. I'm not sure how much you can edit the pyproject.toml directly without it breaking things. For greater control, I'd probably still recommend just using `pip` with `pyproject.toml` combo.


## Useful commands

Install with: `curl -fsSL https://pixi.sh/install.sh | sh`

This creates a whole directory with a `pyproject.toml` file.
`pixi init pixi_hello_world --format pyproject`

Similar, to `python venv -m python3.x` you can specify python versions for your virtual environment like this
```bash
cd pixi_project
pixi add python==3.11.0
python -V # should confirm that it's correct

# Switch to latest
pixi add python
python -V
# Pretty impressive how fast it is and how easily you can switch between them
```

Enter your virtual environment by entering a directory with a `pixi.toml` or `pyproject.toml` or specifying the location to the toml file

```bash
cd pixi_project
pixi shell

# Or
pixi shell --manifest-path /path/to/your/project/<pixi/pyproject>.toml
```

You can see the current list of installed packages in the virtual env for that project by `cd`'-ing in the directory and running `pixi list` or by specifying the pixi or pyproject.toml from elsewhere
```bash
cd pixi_project
pixi list

# Or
pixi list --manifest-file /path/to/your/project/<pixi/pyproject>.toml
```


You can add dependencies to the pixi venv with `cd`'ing to a directory with a pixi or pyproject.toml and then install them like you would with pip
```bash
# either enter the pixi shell to activate the environment
pixi shell

pixi add numpy scipy loguru matplotlib tqdm

# Remove them the same way
pixi remove numpy scipy loguru matplotlib tqdm
```

If the package still appears in the `pixi list` despite removing it, it's because another package is using it as a transitive dependency. Transitive dependencies, I think, are not highlighted in the pixi list whereas properly trued installed packages are.

