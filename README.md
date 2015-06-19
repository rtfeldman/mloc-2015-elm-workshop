Elm Wizardry!
=============

_[mloc.js 2015 Workshop](http://mloc-js.com/2015/#richard_feldman)_

### Installing Elm

The Elm Platform (currently version 0.15) includes everything you'll need for the workshop.

---

* **OS X** users: [download the OS X Elm Installer](http://install.elm-lang.org/Elm-Platform-0.15.pkg)
* **Windows** users: [download the Windows Elm Installer](http://install.elm-lang.org/Elm-Platform-0.15.exe)
* **Other operating system** users: you will unfortunately need to [build from source](http://elm-lang.org/Install.elm#build-from-source). Sorry!

---

Once installation completes, you should be able to run the following:

* `elm-make --version` (This is the Elm compiler. It should be on version 0.1.2)
* `elm-package --version` (This is the Elm package manager. It should be on version 0.5)
* `elm-repl --version` (This is the Elm [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop). It should be on version 0.4)

You may also want to install a [syntax highlighting plugin](http://elm-lang.org/Install.elm#syntax-highlighting) for your favorite editor.

### Set Up Workshop Materials

1. Grab this repository with `git clone https://github.com/rtfeldman/lambdaconf-2015-elm-workshop.git`
2. Run `cd mloc-2015-elm-workshop/1_basic`
3. You should now be in a directory called `1_basic`. Run `ls` to see the contents of this `1_basic` directory; make sure you see these 6 files: `Monsters.elm`, `Wizardry.elm`, `Spells.elm`, `index.html`, `elm-package.json`, and `style.css`.
4. Run `elm-package install` to download and install the project’s dependencies. Answer `y` when prompted `"Do you approve of this plan? (y/n)"`
4. Run `elm-make Wizardry.elm` to compile your program into `elm.js`.
5. Open `index.html` in your browser, which is already set up to load your compiled `elm.js` file. You should see this: ![1_basic](https://cloud.githubusercontent.com/assets/1094080/8247822/0cd1fe92-1657-11e5-8754-2ba0cf6e3cb5.png)
7. From here, you can proceed directly to the [directions for Part 1 of the workshop](https://github.com/rtfeldman/lambdaconf-2015-elm-workshop/tree/master/1_basic), or continue reading below for some useful tips about your Elm development tools.


### Using elm-make and elm-repl

The most direct way to do a build is simply to run `elm-make Wizardry.elm` from within the same directory as the `Wizardry.elm` file. This will generate an output file called `elm.js`, which `index.html` is already configured to load. In a more advanced development environment we would set up automatic recompilcation through a build tool, but for this workshop we will keep our setup simple and just re-run this command each time we want to recompile.

You can also check whether your code compiles from within `elm-repl` before doing a build. To start up the REPL, simply run `elm-repl`. Once inside, enter `import Wizardry` to compile and load `Wizardry.elm` into the current REPL session. When you enter a term into `elm-repl`, it always prints both the value as well as the type; there is no need to separately query for type information. If you enter a function - for example, `List.map`, it will print `<function>` followed by the function's type.

An important caveat is that there is an [open bug](https://github.com/elm-lang/elm-repl/issues/48) where modules that depend directly on elm-html cannot have their terms successfully evaluated in elm-repl. (The error message you'll see is "ReferenceError: navigator is not defined".) So if you do `import Wizardry` and then enter `Wizardry.view`, you will get an error instead of what you want. However, if you do `import Spells` and then enter `Spells.freeze`, or something similar with `import Monsters`, it will work as normal because those modules do not depend on elm-html directly.

If you prefer to do most of your work inside a REPL, you can get a lot of mileage out of working around this by extracting your Model and Action logic into a separate module outside Wizardry.elm; those parts of the code base do not need to depend on elm-html like the view logic does.
