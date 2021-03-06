Commit Messages
---------------

Ensure commit messages have a single title followed by a body as necessary:

```
Short summary text, maximum of 72 characters. That's out to here ---->X

Longer paragraph that details the change and any logic behind needing
to make the change, other impacts, future work etc. Keeping the title
to 72 characters means it will display fully in git log and github logs.
```

Merge commits should not be included in pull requests as they just muddy the history, please rebase when bringing code up to date against latest master.

Code formatting
---------------

To make things easier for everyone, I've adopted clang-format for keeping code consistently formatted. Ensure that your commits are clean against [clang-format-3.8](http://llvm.org/releases/3.8.0/tools/clang/docs/ClangFormatStyleOptions.html). Please avoid making commits which don't follow conventions, and then having a single 'reformatting' commit at the end - this makes history and blames harder to read.

Copyright / Contributor License Agreement
--------------

Any code you submit will become part of the repository and be distributed under the [RenderDoc license](LICENSE.md). By submitting code to the project you agree that the code is your own work and that you have the ability to give it to the project. You also agree by submitting your code that you grant all transferrable rights to the code to the project maintainer, including for example re-licensing the code, modifying the code, distributing in source or binary forms.

Contributing & Development
--------------------------

There are always plenty of things to do, if you'd like to chip in! Check out the [Roadmap](https://github.com/baldurk/renderdoc/wiki/Roadmap) page in the wiki for future tasks to tackle, or have a look at the [issues](https://github.com/baldurk/renderdoc/issues) for outstanding bugs. I'll try and tag things that seem like small changes that would be a good way for someone to get started with.

If you have a change you'd like to see make it into mainline, create a fork of renderdoc, make your changes to a branch, and open a pull request on github. You can look around for instructions on that - it's pretty simple.

We can discuss changes if there need to be any, then merge it in. Please make sure your changes are fully rebased against master when you create the pull request.

If you're tackling anything large then please contact me and post an issue so that everyone knows you're working on it and there's not duplicated effort. *Specifically* if you want to extend RenderDoc to a platform or API that it doesn't already support please get in touch, as there might already be code that isn't committed yet. Particularly if this is not a public API that anyone can write against.

To get started compiling there are instructions in [COMPILE.md](COMPILE.md)

Code of Conduct
--------------

I want to ensure that anyone can contribute to RenderDoc with only the next bug to worry about. For that reason the project has adopted the [contributor covenent](CODE_OF_CONDUCT.md) as a code of conduct to be enforced for anyone taking part in RenderDoc development. If you have any queries in this regard you can get in touch with me [directly over email](mailto:baldurk@baldurk.org).

Code Explanation
--------------

There are [several pages](https://github.com/baldurk/renderdoc/wiki/Code-Dives) on the wiki explaining different aspects of how the code fits together - like how the capture-side works vs replay-side, how shader debugging works, etc.

    renderdoc/ 
        Makefile                        ; The linux make file, will recurse into subdirectories to build them
        renderdoc.sln                   ; VS2010 solution for windows building
        renderdoc/
            3rdparty/                   ; third party utilities & libraries included
            drivers/                    ; API-specific back-ends, can be individually skipped/removed
            ...                         ; everything else in here consists of the core renderdoc runtime
        renderdoccmd/                   ; A small C++ utility program that runs to do various little tasks
        renderdocshim/                  ; A tiny C DLL using only kernel32.dll that is used for global hooking
        renderdocui/                    ; The .NET UI layer built on top of renderdoc/
            3rdparty/                   ; third party utilities & libraries included
        qrenderdoc/                     ; The Qt UI layer built on top of renderdoc/
        pdblocate/                      ; a simple stub program to invoke DIA to look up symbols/pdbs
                                        ; for callstack resolution on windows
        docs/                           ; source documentation for the .chm file or http://docs.renderdoc.org/
                                        ; in the Sandcastle help file builder
        installer/                      ; installer scripts for WiX Toolset
        dist.sh                         ; a little script that will build into dist/ with everything necessary
                                        ; to distribute a build - assumes that exes etc are already built

Testing
--------------

At the moment the testing of any features and changes is pretty much ad-hoc. I've been working on a proper test suite that will test both API capture/replay support as well as the analysis features.

Until then, test any changes you make around the area that you've tested - if I have any particular suggestions on testing I will probably bring it up in the pull request.
