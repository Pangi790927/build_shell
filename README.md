# build_shell

random idea that came to my mind and I wanted to save it, it's a jumbled mess(I've just written
whatever came to my mind, with no regard to anything), but whatever, maybe some day I will work on it:


bsh - build shell (not really a shell, more like a kernel extension, better name needed)

The idea is to have a shell that records whatever steps where done to build a repository and
remember those steps. Whenever you add things to a project you use this shell. In the background,
the shell isolates all commands such that no library, file, etc. is used outside the build process.
All the tools used in the process need to be either a specific set of tools that are known, or tools
that can be downloaded and built. In the end you will be able to take the recorded project and cross
compile it for whatever you need, as long as the required steps where done only in the shell. The
building steps will be available for evaluation and commited before adding them, similar to git.

So for example if you do something like this:

cd project
mkdir build
mkdir no-reason
cmake .. -some-options
make
make install
!save           <- this is the step in the shell that saves the thing

Then this should open a new window that lets you remember this set of instructions, edit them, for
example by removing "mkdir no-reason" and save them as a command, for example build-install-project.
This command will be saved and all the changes will be recorded and undo-able(file moving, editing,
creating, link creating, etc.).

!save <save-point> -> saves the list of commands after letting you edit them
!undo -> reverses the last command (for example can reverse 'apt install something' properly)
!reverse <optional:save-point> -> removes the last commands till a save-point is reached
!exec <save-point> -> executes save point, if it depends on prev steps, also exec those
!menu -> opens app menu for other stuff

Save points, based on some rules can depend on other save points or be independent. In the end,
everything is saved to a project file (only one of those) and you can take this file and move it
wherever you like, such that in the future you will be able to exec any command of those recorded
and recreate the project as such. If needed all steps can be replaced and all utils can also be
replaced, either by referencing them or by recompiling them. No change is permited outside the shell,
except some specific file types. gitignore can be updated from the shell, include paths can be found
in the shell, .so, libs, etc. also can be found, steps can be listed for a command, for example to see
exactly what an install has done to the system. If directory is watched(kext), then no random file
appears inside the directory and no install can interfere, meaning that you can finally ensure all
dependencies, no exception.

This program should also be able to import another set of such rules, ie take the file and integrate
it.

This program should also have some helper importable presets, for building some of the stuff.
