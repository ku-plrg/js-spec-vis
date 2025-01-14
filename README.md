# JSSpecVis: A JavaScript Language Specification Visualization Too

JSSpecVis is a tool that visualizes the JavaScript language specification
([ECMA-262](https://tc39.es/ecma262/)). It extends
[ESMeta](https://github.com/es-meta/esmeta) tool-chain to extract the
mechanized specification from ECMA-262 and visualize it in a web browser.


## Installation Guide

We explain how to install JSSpecVis with the necessary environment settings from
scratch. Our framework is developed in Scala, which works on JDK 17+. So before
installation, please install [JDK
17+](https://www.oracle.com/java/technologies/downloads/) and
[sbt](https://www.scala-sbt.org/), an interactive build tool for Scala. And, you
need [npm](https://www.npmjs.com/) to run the program visualizer and client-side
of double debugger.


### Download JSSpecVis
```bash
$ git clone https://github.com/ku-plrg/js-spec-vis.git
```

### Environment Setting

Insert the following commands to `~/.bashrc` (or `~/.zshrc`):
```bash
# for JSSpecVis
export ESMETA_HOME="<path to JSSpecVis>" # IMPORTANT!!!
export PATH="$ESMETA_HOME/bin:$PATH" # for executables `js-spec-vis` and etc.
source $ESMETA_HOME/.completion # for auto-completion
```
The `<path to JSSpecVis>` should be the absolute path of the JSSpecVis
repository.


### Installation of JSSpecVis using `sbt`

Please type the following command to 1) update the git submodules, 2) generate
binary file `bin/js-spec-vis`, and 3) apply the `.completion` for
auto-completion.

```bash
$ git submodule update --init && sbt assembly && source .completion
```

If you see the following message, JSSpecVis is successfully installed:
```bash
$ js-spec-vis
# Welcome to JSSpecVis v1.0.0 - A JavaScript Language Specification Visualization Tool.
# Please type `js-spec-vis help` to see the help message.
```


## Usage Guide

JSSpecVis consists of three main components: 1) **Program Collector** as a
preprocessor, 2) **Program Visualizer** for browsing the collected programs, and
3) **Double Debugger** for interactive execution of JavaScript programs on the
specification.


### Program Collector

First, you need to collect example programs from the mechanized specification of
ES2024.


### Program Visualizer

TODO


### Double Debugger
