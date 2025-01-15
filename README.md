
# <span style="color: red;">&#10060; </span> sqlalchemy.exc.OperationalError :  
**(psycopg2.OperationalError) connection to server at** **"dpg-cu3sasrtq21c73ar161g-a.oregon-postgres.render.com" (35.227.164.209), port** **5432 failed: Connection timed out (0x0000274C/10060)**
**Is the server running on that host and accepting TCP/IP connections?**`
## Solution:
1. Uninstall the current `psycopg2` package:
   pip uninstall psycopg2
   pip install psycopg2-binary


# <span style="color: red;">&#10060; </span> Handling `ModuleNotFoundError` in FastAPI 

**When working with a FastAPI project, you may encounter a `ModuleNotFoundError` if your project structure and configuration are not correctly set up for Python to locate your modules. This guide demonstrates how to resolve this issue using `setuptools` and a `setup.py` file.**

## Example Error

Imagine the following project structure:

```
my_project/
├── src/
│   ├── my_app/
│   │   ├── __init__.py
│   │   ├── main.py
│   ├── __init__.py
├── tests/
├── setup.py
```

Running the `main.py` file may raise this error:

```
ModuleNotFoundError: No module named 'my_app'
```

This happens because Python cannot find the `my_app` module unless it is explicitly included in the Python path.

## Solution: Using `setuptools`

To ensure your module is properly recognized, you can use `setuptools` to package your project. Here’s how to do it:

### Step 1: Create or Modify `setup.py`

Ensure your `setup.py` file is configured as follows:

```python
from setuptools import setup, find_packages

setup(
    name="my_project",
    version="0.1.0",
    packages=find_packages(where="src"),
    package_dir={"": "src"},
    install_requires=["fastapi", "sqlalchemy"],
)
```


### Step 2: Install Your Project Locally

Run the following command in the terminal at the root of your project:


pip install -e .


This command installs your project in editable mode. Editable mode means any changes to your source code are immediately reflected without needing to reinstall.

### Step 3: Run Your Application

now it should work without raising the `ModuleNotFoundError`.

### Step 4: Use Direct Imports

After setting up your project with `setuptools`, you can now use direct imports in your code. For example, instead of relative imports like:

from .some_module import some_function

you can directly import modules using their package names:

from my_app.some_module import some_function

This makes your code cleaner and more maintainable.

## Additional Notes

- Ensure all necessary modules have an `__init__.py` file, marking them as packages.
- Use `find_packages(where="src")` in `setup.py` to locate the modules inside the `src` directory.
- Use `pip install -e .` during development to avoid repeating installations after each change.

By following these steps, you can resolve `ModuleNotFoundError` issues in FastAPI projects and improve the organization of your codebase.

