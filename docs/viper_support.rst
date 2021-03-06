Viper Support
=============

Populus has support for the `viper <https://github.com/ethereum/viper>`_
compiler. Viper is a python-like experimental programming language.


Known limitations
-----------------

Viper requires Python 3.6 or above.


Installation
------------

To install the compiler:


.. code-block:: shell

   pip install https://github.com/ethereum/viper/archive/master.zip


You will see the `viper` binary is now installed.


.. code-block:: shell

    $ viper
    usage: viper [-h] [-f {abi,json,bytecode,bytecode_runtime,ir}]
                 [--show-gas-estimates]
                 input_file
    viper: error: the following arguments are required: input_file


Using
-----

To use it as your compiler backend the `project.json` file must be modified.
Place a `backend` key in the `compilation` section, as shown below:


.. code-block:: json

    {
        "version": "8",
        "compilation": {
            "contracts_source_dirs": ["./contracts"],
            "import_remappings": [],
            "backend": {
                "class": "populus.compilation.backends.ViperBackend"
            }
        }
    }


This will set the Populus framework to only pick up Viper contracts in the
configured contracts directories.
Now that everything is configured you can create a Viper greeter contract:


.. code-block:: python

    # contracts/Greeter.v.py

    greeting: bytes <= 20


    @public
    def __init__():
        self.greeting = "Hello"


    @public
    def setGreeting(x: bytes <= 20):
        self.greeting = x


    @public
    def greet() -> bytes <= 40:
        return self.greeting


And run the default Populus tests:

.. code-block:: shell

    py.test
