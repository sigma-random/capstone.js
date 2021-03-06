Capstone.js
===========
[![Last Release](https://badge.fury.io/gh/AlexAltea%2Fcapstone.js.svg)](https://github.com/AlexAltea/capstone.js/releases)

Port of the [Capstone](https://github.com/aquynh/capstone) disassembler framework for JavaScript. Powered by [Emscripten](https://github.com/kripken/emscripten).

**Notes:** _Capstone_ is a lightweight multi-architecture disassembly framework originally developed by Nguyen Anh Quynh and released under BSD license. More information about contributors and license terms can be found in the files `CREDITS.TXT` and `LICENSE.TXT` of the *capstone* submodule in this repository.

## Installation
To install the Capstone.js install in your web application, include it with:
```
<script src="capstone.min.js"></script>
```
or installer through the Bower command:
```
bower install capstone
```

## Usage                                                      
```javascript
// Input: Machine code bytes and offset where they are located
var buffer = [0x55, 0x48, 0x8b, 0x05, 0xb8, 0x13, 0x00, 0x00];
var offset = 0x1000;

// Initialize the decoder
var cs = new capstone.Cs(capstone.ARCH_X86, capstone.MODE_64);

// Output: Array of capstone.Instruction objects
var instructions = cs.disasm(buffer, offset);

// Display results;
instructions.forEach(function (instr) {
    console.log("0x%s:\t%s\t%s",
        instr.address.toString(16),
        instr.mnemonic,
        instr.op_str
    );
});

// Delete decoder
cs.delete();
```

## Building
To build the Capstone.js library, clone the *master* branch of this repository, and do the following:

1. Initialize Git submodules to fetch the original Capstone repository: `git submodule update --init`.

2. Install the development and client dependencies with: `npm install` and `bower install`.

3. Install the lastest [Python 2.x (64-bit)](https://www.python.org/downloads/), [CMake](http://www.cmake.org/download/) and the [Emscripten SDK](http://kripken.github.io/emscripten-site/docs/getting_started/downloads.html). Follow the respective instructions and make sure all environment variables are configured correctly. Under Windows [MinGW](http://www.mingw.org/) (specifically *mingw32-make*) is required.

4. Finally, build the source with: `grunt build`.
