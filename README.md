# JSSpecVis: A JavaScript Language Specification Visualization Tool

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
ES2024. It consists of three phases: 1) fuzzing, 2) executing test262, 3)
collecting the programs.

However, fuzzing require tens of hours to collect the programs, and executing
test262 require more than 10 minutes. So, we provide three options to collect
the programs.


#### 1. Use Pre-collected Dataset

> :note:
> 
> We highly recommend using the pre-collected dataset to save your time.

The easiest way to use JSSpecVis is to use the pre-collected dataset.
First, unzip the `resources.tar.gz` file:

```bash
tar -xzvf resources.tar.gz
```

Then, move the `resources` directory to the visualizer public directory:
```
mv resources visualizer/public/
```


#### 2. Start from Fuzzing Results

It assumes that the mutation-based fuzzing is completed, and the results are
stored in the `fuzz-data.tar.gz` file. First, unzip the `fuzz-data.tar.gz` file:

```bash
tar -xzvf fuzz-data.tar.gz
```

Then, move the `fuzz-data` directory to `logs/fuzz/recent` directory:
```
rm -f logs/fuzz/recent && mv fuzz-data logs/fuzz/recent
```

Then, run the following command to collect Test262 programs:

```bash
js-spec-vis test262-test -test262-test:progress -test262-test:log -test262-test:concurrent=0 -test262-test:total-coverage
```

And, collect the programs:

```bash
js-spec-vis collect
```

Finally, move the `logs/fuzz/recent/json-dump` directory to the visualizer
public directory:

```bash
mv logs/fuzz/recent/json-dump visualizer/public/resources
```



#### 3. Collect Programs by Yourself


This is the most time-consuming option. If you want to collect the programs
by yourself, please follow the instructions below.

First, you need to run the following command to run the mutation-based fuzzing:

```bash
js-spec-vis fuzz -fuzz:log -fuzz:cp -fuzz:k-fs=1
```

The `-fuzz:k-fs=1` option denotes 1-FS coverage, and `fuzz:cp` option denotes
FCPS coverage. So, this combination denotes 1-FCPS coverage.

Then, similar to the previous option, run the following command to collect
Test262 programs:

```bash
js-spec-vis test262-test -test262-test:progress -test262-test:log -test262-test:concurrent=0 -test262-test:total-coverage
```

And, collect the programs:

```bash
js-spec-vis collect
```

Finally, move the `logs/fuzz/recent/json-dump` directory to the visualizer
public directory:

```bash
mv logs/fuzz/recent/json-dump visualizer/public/resources
```

### Program Visualizer

TODO


### Double Debugger
