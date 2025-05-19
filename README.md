### MULTITHREADED ZIP FILES CRACKER BY THOMAS (OR DEEDEE) ###

### Quick tutorial: (idk why i named the package and the class the same way hahaa)

    zipcracker.zipcracker(func,
    	passfile,
    	numthreads=4,
    	cont=False,
    	mode=ROUND_ROBIN)

* **func**: A function that returns `True` if the password is correct, `False` otherwise. The only parameter passed to it is the password to try.
* **passfile**: The file to read newline-separated passwords from.
* **numthreads**: Number of threads to start. Default 4.
* **cont**: Boolean value to continue looking if a password is found.
* **mode**: Selects the mode of distribution of the passwords to each thread.


### MODES: ###

`ROUND_ROBIN`: distributes passwords in a round-robin distribution:

    1    2    3    4
    5    6    7    8 ...

**currently unimplemented** `SEGMENTED`: segments the password file equally among threads:

    1   100  200  300
    2   101  201  301 ...

The actual work is done during the call to `run()`. This function will return a list of passwords found to be correct.

### EXTENDED: ###

There is also an extended "mode" of operation.
Zipcracker_extended, which will require more user side code, but is more powerful. Each thread instantiates its own class, which allows there to be persistent objects across all attempts in each thread.

To use simply substitute your custom class for the `func` variable during initialization. It needs to extend the `zippycrack.xdefault` class, with three optional functions overridden:

* `__init__(self,tid)` - called on initialization, `tid` is thread ID
* `run(self,pwd)` - called once per password, `pwd` is the password. as before, return `True` to indicate success
* `done(self)` - called on completion, use to clean up stuff

_In the 'examples' folder, there is a real test case as an example for users._
