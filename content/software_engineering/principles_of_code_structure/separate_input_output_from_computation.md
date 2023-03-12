+++
title = "Separate Input/Output From Computation"
date = 2022-12-19
weight = 90
+++

# Separate Input/Output From Computation

A lot of computer code follows the pattern handed down to us from the ancients:
1. Get some data from somewhere.
2. Do some computations from the data to produce new data.  Equivalently, _transform_ the data.
3. Put the new data somewhere.

Separate the code that does Input or Output into its own modules.  Do _not_ make an I/O call in the middle of some code that is doing a computation.

An Input code module deals with things like reading a configuration file, reading environment variables from the operating system, loading data from a file, _et cetera_.

An Output code module will typically handle writing to a file or database, or transferring data through a network call.

Rules of thumb for readable code:
1. Try to put the calls to the Input module at the beginning of the program.
2. Try storing the input data in some kind of State module, for later use.
3. Try to put he calls to the Output module at the end of the program.

Input and Output are major dependencies of the program.  For example, a program may depend on the existence of a config file as input.  Now suppose the config variables are not needed until half way through the program.  An 'efficient' programmer might delay reading the config file until the point at which it is needed.  However, it is better to read the config file at the very beginning of the program, because:
1. It makes the dependency on the existence of the config file immediately explicit to the reader.
2. If the file is missing, the program will error immediately, instead of wasting time on a computation that will ultimately fail.

Make dependencies explicit.  Declare them early; your readers will want to know about them.  Fail early.  Make sure you have everything that you need before starting the job.
