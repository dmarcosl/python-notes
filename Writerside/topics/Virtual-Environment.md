# Virtual Environment

A Python virtual environment **isolates dependencies and packages**, ensuring projects have **independent and conflict-free setups**.

Unlike `node_modules` in `Node.js` or `vendor/bundle` in `Ruby`, it also contains the **Python interpreter**.

## Creating a Virtual Environment

To create a new virtual environment, use the following command:

```bash
python -m venv [path]
```

Examples:

```bash
python -m venv /home/user/myenv
python -m venv my_virtual_environment
```

## Activating the Virtual Environment

To use the Python interpreter from the virtual environment instead of the system-wide installation, you need to activate it.

In the `bin` folder inside the virtual environment directory, you'll find the activation script. Use one of the following commands:

```bash
. [path]/bin/activate
```

Examples:

```bash
. /home/user/myenv/bin/activate
. my_virtual_environment/bin/activate
```

To deactivate the virtual environment and return to the system-wide Python installation, run:

```bash
deactivate
```

When the virtual environment is activated, the command line prompt will show the environment name on the left, like this:

```bash
(myenv) user@machine:path$ 
```