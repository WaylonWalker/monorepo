A python monorepo created with hatch.


## Configuration

This configuration goes in your global hatch config, you can find it with
`hatch config find`.


``` toml
[projects]
one = '/home/waylon/git/monorepo/project-one'
two = '/home/waylon/git/monorepo/project-two'
three = '/home/waylon/git/monorepo/project-three'

[dirs]
project = ["/home/waylon/git/monorepo"]
```

## Editable installs

I am looking for a good way to make all the projects able to editable install
each other.  This will allow quick updates without needing a new venv. Go to
definition will now just work, rather than going into the projects venv, it
will take you to the real source code that you can safely edit.


### Currently scripts work


``` toml
[tool.hatch.envs.default.scripts]
editable = [
    "python -m pip install -e ../project-one",
    "python -m pip install -e ../project-two",
]
```

``` bash
hatch -p three run editable
## or you can run it locally to the project
cd project-three
hatch run editable
```

### Better

It would be better for this to be seemless, either by specifying the dependency
as editable in the dependency section, or in a pre/post install command.
Currently these are not working for me.

## Links

* Hatch [#233](https://github.com/pypa/hatch/issues/233) - Monorepo support
* Hatch Docs [post-install config](https://hatch.pypa.io/latest/config/environment/overview/#post-install)
* Requirements.txt [plugin](https://github.com/repo-helper/hatch-requirements-txt)

