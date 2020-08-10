Pyre is a performant type checker for Python compliant with PEP 484. Pyre can analyze codebases with millions of lines of code incrementally – providing instantaneous feedback to developers as they write code.

Pyre ships with Pysa, a security focused static analysis tool we've built on top of Pyre that reasons about data flows in Python applications. Please refer to our documentation to get started with our security analysis.

Requirements
To get started, you need Python 3.6 or later and watchman working on your system. On MacOS you can get everything with homebrew:

$ brew install python3 watchman
On Ubuntu, Mint, or Debian; use apt-get:

$ sudo apt-get install python3 python3-pip watchman
We tested Pyre on Ubuntu 16.04 LTS, CentOS 7, as well as OSX 10.11 and later.

Setting up a Project
We start by creating an empty project directory and setting up a virtual environment:

$ mkdir my_project && cd my_project
$ python3 -m venv ~/.venvs/venv
$ source ~/.venvs/venv/bin/activate
(venv) $ pip install pyre-check
Next, we teach Pyre about our new project:

(venv) $ pyre init
This command will set up a configuration for Pyre (.pyre_configuration) as well as watchman (.watchmanconfig) in your project's directory. Accept the defaults for now – you can change them later if necessary.

Running Pyre
We are now ready to run Pyre:

(venv) $ echo "i: int = 'string'" > test.py
(venv) $ pyre
 ƛ Found 1 type error!
test.py:1:0 Incompatible variable type [9]: i is declared to have type `int` but is used as type `str`.
This first invocation will start a daemon listening for filesystem changes – type checking your project incrementally as you make edits to the code. You will notice that subsequent invocations of pyre will be faster than the first one.

For more detailed documentation, see https://pyre-check.org.
