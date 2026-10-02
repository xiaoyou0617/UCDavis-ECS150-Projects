# ECS 150 programming projects

These projects are meant to get you warmed up with programming in the C++/UNIX
environment. None are meant to be particularly hard, but should be enough so
that you can get more comfortable programming. 

Realize the best thing you can do to learn to program in any environment is to
program **a lot**. These small projects are only the beginning of that
journey; you'll have to do more on your own to truly become proficient.

* [Unix Utilities](project1)
* [Unix Shell](project2)
* [Concurrent Web Server](project3)

Tip of the hat to Remzi and Andrea Arpaci-Dusseau for the amazing
[textbook](https://pages.cs.wisc.edu/~remzi/OSTEP/) and
[projects](https://github.com/remzi-arpacidusseau/ostep-projects),
which we borrow from heavily.

# Using Visual Studio Code and Docker

In this class, the supported configuration is to install Docker Desktop and Visual
Studio Code on your local computer, or to use the Visual Studio Code instances
on the CSIF lab machines.

## Installation
To install these packages, follow the installation instructions [here](https://code.visualstudio.com/docs/devcontainers/containers).
We already have your devcontainer and other settings configured, and Visual Studio
Code will manage Docker for you, but the instructions have links to instructions for
installing Docker on Windows, Mac, and Linux machines.

## Concepts
Conceptually, Visual Studio Code is an application running on your computer. It creates a virtual machine,
using Docker, that has the right version of Linux for this class. Visual Studio Code
handles synchronization between files on your local computer and the virtual machine
and exposes a terminal where you can use the command line to interact with your code
running within the virtual machine, which is also called a dev container.

In a typical configuration you will edit your code using Visual Studio Code, and
compile and run your code using the terminal.

To debug your code using the Visual Studio Code debugger, you need to run your
program using the terminal and then use one of our pre-set configurations to
attach to your running program. Conceptually, there is a server running in your
container that manages the Linux side of debugging, and Visual Studio Code connects
to this server to issue debugging commands and display the state of your program
within the editor.

## Debugging
To debug a program, you run it as follows:

_For Projects 1 and 2 compile with the `-g` flag_
* ```g++ -g -o wcat -Wall -Werror wcat.cpp```

_For Projects 3 and 4 compile it without address sanitizer_
* ```make clean; DEBUGGER=true make```

_In the Visual Studio Code terminal run the program you want to debug_
* [Linux, Windows, Mac (x86) host] ```gdbserver localhost:1234 ./wcat```
* [Mac (Apple Silicon) host] ```ROSETTA_DEBUGSERVER_PORT=1234 ./wcat```

_Then in Visual Studio Code editor_
* Select the main file for the program you want to debug (e.g., `wcat.cpp`) in the Editor. The debugger uses this file to find the program you want to debug.
* Select "Run and Debug" on the left hand control pane
* Select the "GDB Debug Current File" configuration and hit the play button

This will connect your Visual Studio Code debugger to your program running in your container.

## What if Docker or the debugger doesn't work?

We added a debug target for Mac hosts that will use the Mac native
debugger without Docker. Note, this configuration is not supported,
but if you're stuck and just need to get your project done many have
had success with it. To use it you:
* Open your project and _do not_ open in a dev container.
* On the terminal, compile with `make clean; DEBUGGER=true make`
* Make sure that the utility you want to debug is visible in your editor. For example, if you're debugging `ds3cat` then `ds3cat.cpp` should be open in your editor.
* Go to the VSCode debugger panel and select the "Mac Native Debug Current File" option.
* **Important** If you're seeing inconsistencies between your Mac
  and the autograder, try running your code on a CSIF machine, which
  you can access using SSH. The CSIF machine are running the same
  version of Linux that the autograder uses, so should provide a
  good way to run a final check on your code if you're facing issues.

## Hints
Here are a few hints to help, but Visual Studio Code is widely used software so checking
online for help when you get stuck will be useful:
* Select "Auto Save" in Visual Studio Code to ensure that it saves your files as you edit.
* In our examples we use port `1234` for the debugger, but you can change this port if needed, just make sure that you update your `launch.json` file to match.
* To get started with a project, you will typically clone this repo using Visual Studio Code "Clone git repository" option and Visual Studio Code will set up a Dev Container for you based on the confiugrations we included in that repo.
* If we push an update in the middle of a project, you can use `git pull` in your host terminal to fetch the latest updates. There is probably a way to do this in Visual Studio Code as well.
* If you're using a Mac with Apple Silicon, make sure to enable both the "Apple Virtualization Framework" and "Use Rosetta for x86_64/amd64 emulation on Apple Silicon" options in Docker Desktop
