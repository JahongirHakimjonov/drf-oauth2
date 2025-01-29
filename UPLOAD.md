To upload the new version of your package to PyPI, follow these steps:

1. **Ensure your package is ready**: Make sure all changes are committed, and your package is in a stable state. Update the version number in `setup.py` if you haven't already. It looks like you've set the version to `0.0.5`.

2. **Build your package**: You need to create a distribution package. This can be done using `setuptools`. Run the following commands in your terminal:

```bash
python setup.py sdist bdist_wheel
```

This command generates a source distribution (`sdist`) and a wheel (`bdist_wheel`).

3. **Upload your package to PyPI**: You can use `twine` to upload your package. If you haven't installed `twine`, you can do so using pip:

```bash
pip install twine
```

Then, upload your package by running:

```bash
twine upload dist/*
```

This command will prompt you for your PyPI username and password.

4. **Verify**: After uploading, check your package on PyPI to ensure it's correctly updated.

Remember, every time you upload a new version, you should increment the version number in `setup.py` and rebuild your package before uploading.