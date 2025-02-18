# Execution and Interaction

There are three ways to try Python code:

- Creating a `.py` file and executing it with `python script.py`.
- Using **IPython**, a Python shell.
- Using **Jupyter Notebook**, a web-based interactive environment.

## IPython

IPython is an interactive shell for Python that provides rich features like syntax highlighting.

After creating and activating a virtual environment, install IPython with:

```bash
pip install ipython
```

Then open it by one of the next two commands:

```bash
ipython
```

```bash
venv/bin/ipython
```

Now you can start trying writing python code in the interactive shell, for example:

```python
hello = 'Hello from IPython!'
hello
```

It has special commands like these:

```python
%time sum(range(1000000))  # Measures execution time
%history                   # Shows command history
exit                       # Exits from IPython
```

## Jupyter Notebook

Jupyter Notebook is a web-based tool that allows users to create and run interactive Python notebooks with code, text, and visualizations.

To install it:

```bash
pip install jupyter
```

To open it:

```bash
jupyter notebook
```

```bash
venv/bin/jupyter notebook
```

This will open a new tab in the browser. To create a new notebook go to File > New > Notebook, then open the new created file.

Here you can create cells with code and execute it with **ctrl + enter**, for example:

```python
hello = 'Hello from the Notebook!'
hello
```