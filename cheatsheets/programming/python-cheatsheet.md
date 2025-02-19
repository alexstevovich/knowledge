# Install an Editable Package

``` sh
#install:
pip install -e .

#uinstall:
pip uninstall my_package
```

This command tells pip to install the package in editable mode. It essentially creates a link from the site-packages directory to your package's source code. As a result, you can freely develop your package and test it across different projects on your system without having to reinstall it after each change.

# PYLINT

Pylint, a widely used static code analysis tool for Python. Static code analysis involves checking your source code for potential errors, stylistic issues, and deviations from coding standards without actually executing the program. Pylint examines Python code to enforce coding standards and look for programming errors, helping developers to identify and fix problems early in the development process. It can catch errors that are not syntax errors but may cause bugs in the program, suggest improvements for code readability, and enforce a coding standard across a project.

``` sh
pip install pylint
```

``` sh
pylint example.py
```

### Trim White Spaces
Use VSCodes native **"Trim White Spaces"** command from the command palette. (See the VSCode Cheetsheet for details.)


### Skipping instances of linting:

In very specific situation like this I've felt the need to bypass linting. It's a package __init__ file in which I did not want to expose my_class as part of the package interface, and only expose the get_instance_of_my_class() function. 

``` py
#package __init__.py file
def get_instance_of_my_class():
    # pylint: disable=import-outside-toplevel
    import my_class
    instance = my_class.MyClass()
```

This however could also be handeled by simply hinting that the package is private:

``` py
#package __init__.py file
from . import apply_components_task as _apply_components

def get_instance_of_my_class():
    instance = my_class.MyClass()
```