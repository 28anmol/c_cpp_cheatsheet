# C/C++ Cheatsheet

*An important documentation which runs through most important compilation commands for C/C++ through CLI, concept of Make, Makefiles, CMake and CMakeLists.txt. WIP...*

C++ is mostly backward compatible with C: most of the C code/syntax is supported in a c++ file. All the codes written in C/C++ are stored in your storage but when you execute them, all variable memory allocation, execution of the program is done on RAM itself.

Tools needed for running C/C++ code on your system:
- Text Editor(VS Code)
- C/C++ compiler(GNU GCC/Clang)

C and C++ have evolved since inception in many iterations/versions and different compilers support different C/C++ versions so please make sure which language version you want to use. Download the compiler version accordingly.


This repository will mostly focus on the following aspects:
- C/C++ project file structure
- C/C++ compilation steps
- Terminal commands to handle compilation of C/C++ source code
- Other helpful terminal commands to check versions of compiler, C/C++ Standard
- `make` and `cmake` commands and their working
- Makefile file basics


### C/C++ Project Folder Structure

```bash
project-name/
├── build/               # Build output (ignored by git)
├── bin/                 # Bin file contains binaries
├── include/             # All header files (.h)
│   ├── utils.h
│   └── module1.h
├── src/                 # All source files (.c)
│   ├── main.c
│   ├── utils.c
│   └── module1.c
├── tests/               # Unit tests or test programs
│   └── test_utils.c
├── docs/                # Documentation, if any (optional)
├── examples/            # Example programs or usage demos (optional)
├── Makefile             # Build automation script
├── CMakeLists.txt       # CMake build script (optional)
├── README.md            # Project overview and instructions
├── .gitignore           # To exclude build/, binaries, etc.
└── LICENSE              # License file (optional but recommended)
```


```bash
project-name/
├── build/                # Build output (ignored by git)
├── bin/                 # Bin file contains binaries
├── include/              # Header files (.hpp/.h)
│   ├── utils.hpp
│   └── module1.hpp
├── src/                  # Source files (.cpp)
│   ├── main.cpp
│   ├── utils.cpp
│   └── module1.cpp
├── tests/                # Unit tests or test programs
│   └── test_utils.cpp
├── examples/             # Example usage programs (optional)
├── docs/                 # Documentation (optional)
├── CMakeLists.txt        # CMake build script (recommended for C++)
├── Makefile              # Optional, for simple build automation
├── README.md             # Project description
├── .gitignore            # Ignore build files, binaries, etc.
└── LICENSE               # License (optional)
```

```graphql
project-name/
├── build/                      # 🔧 Build output (excluded in .gitignore)
├── bin/                        # 🗃️ Final binaries go here
├── lib/                        # 📦 Compiled static/shared libraries
├── include/                    # 🌐 Public headers (for library users)
│   └── project_name/           # Namespaced includes (e.g., <project_name/foo.h>)
│       ├── project.h
│       ├── utils.h
│       └── module1.h
├── src/                        # 💻 Internal source files
│   ├── main.c / main.cpp       # Entry point (if building app)
│   ├── project.c / .cpp        # Shared library logic
│   ├── utils.c
│   └── module1.c
├── internal/                   # 🚫 Private/internal headers (non-installed)
│   ├── config.h
│   └── defs.h
├── examples/                   # 🧪 Example programs using your library
│   ├── example1.c
│   └── example2.cpp
├── tests/                      # ✅ Unit & integration tests
│   ├── test_main.c
│   ├── test_utils.c
│   └── mocks/
│       └── mock_file_io.c
├── tools/                      # 🛠️ Helper scripts (formatting, codegen, etc.)
│   ├── format.sh
│   └── ci_build.sh
├── cmake/                      # ⚙️ Custom CMake modules/macros
│   └── FindMyDep.cmake
├── docs/                       # 📚 Documentation (API, diagrams, architecture)
│   ├── README.md
│   ├── API.md
│   └── diagrams/
│       └── arch.png
├── .vscode/                    # 🧠 VSCode configs (optional)
│   ├── settings.json
│   ├── tasks.json
│   └── launch.json
├── .gitignore                  # 🚫 Ignore rules (build/, *.o, *.bin, etc.)
├── README.md                   # 🏁 Project overview, build instructions, usage
├── LICENSE                     # 🧾 License file
├── Makefile                    # 🧱 Optional: legacy/simple builds
├── CMakeLists.txt              # 📐 Top-level CMake file
└── package/                    # 📦 Optional: build artifacts for distribution
    ├── include/
    ├── lib/
    ├── README.md
    └── version.txt
```


```graphql
project-name/
├── build/                      # Build output directory (gitignored)
├── bin/                        # Compiled binary executables
├── lib/                        # Static/shared library output
├── cmake/                      # CMake helper modules/macros
│   └── FindSomeDependency.cmake
├── config/                     # Config files, e.g. JSON/XML/toml
│   └── default_config.json
├── docs/                       # Documentation (Markdown or Doxygen)
│   ├── index.md
│   └── diagrams/
│       └── system_architecture.puml
├── examples/                   # Example apps/demos using your library
│   ├── minimal.cpp
│   └── advanced.cpp
├── external/                   # External libraries (submodules or downloaded)
│   └── catch2/
├── include/                    # Public headers for your library (installed)
│   └── project_name/
│       ├── project.hpp
│       ├── module1.hpp
│       └── utils.hpp
├── internal/                   # Private/internal headers
│   ├── pch.hpp                 # Precompiled headers
│   └── detail/
│       └── unsafe_impl.hpp
├── modules/                    # C++20 module files (if applicable)
│   ├── project_name.ixx
│   └── math_utils.ixx
├── src/                        # Library + Application sources
│   ├── main.cpp                # Entry point (optional CLI app)
│   ├── project.cpp
│   ├── module1.cpp
│   └── utils.cpp
├── tests/                      # Unit and integration tests
│   ├── test_main.cpp
│   ├── test_module1.cpp
│   └── mocks/
│       └── fake_logger.hpp
├── tools/                      # Scripts and tooling (linters, codegen, etc.)
│   ├── generate_docs.sh
│   └── run_static_analysis.py
├── scripts/                    # Build, install, deploy scripts
│   ├── build_debug.sh
│   ├── build_release.sh
│   └── ci_setup.sh
├── .vscode/                    # VSCode settings (optional)
│   ├── settings.json
│   ├── launch.json
│   └── tasks.json
├── .github/                    # GitHub actions (CI/CD workflows)
│   └── workflows/
│       └── build.yml
├── .gitignore                  # Ignore build/, logs, etc.
├── CMakeLists.txt              # Top-level CMake
├── README.md                   # Project description & usage
├── LICENSE                     # License file (MIT, Apache, etc.)
└── Doxyfile                    # Doxygen config file (optional)
```

```graphql
project-name/
├── build/                      # 🔧 All build artifacts (ignored by Git)
├── bin/                        # 🏁 Final executables (.out, .elf)
├── lib/                        # 📦 Compiled libraries (.a, .so)
├── obj/                        # 🔩 Intermediate object files (.o)
├── cmake/                      # ⚙️ CMake helper modules/macros
│   └── FindCustomLib.cmake
├── config/                     # ⚙️ JSON/TOML/XML configuration files
│   └── default_config.json
├── docs/                       # 📚 Documentation (Markdown or Doxygen)
│   ├── README.md
│   └── diagrams/
│       └── architecture.png
├── examples/                   # 🧪 Example programs showing how to use your library
│   ├── minimal.c
│   └── advanced_usage.c
├── external/                   # 🧩 External dependencies (manually or via submodules)
│   └── cmocka/
├── include/                    # 🌐 Public header files (installed with lib)
│   └── project_name/
│       ├── project.h
│       ├── module1.h
│       └── utils.h
├── internal/                   # 🚫 Private headers (used only inside project)
│   ├── config.h
│   └── detail/
│       └── unsafe_impl.h
├── src/                        # 💻 C source files
│   ├── main.c                  # Entry point (for CLI apps)
│   ├── project.c
│   ├── module1.c
│   └── utils.c
├── tests/                      # ✅ Unit and integration tests
│   ├── test_main.c
│   ├── test_module1.c
│   └── mocks/
│       └── mock_io.c
├── tools/                      # 🛠️ Helper scripts/tools (e.g. codegen, style checks)
│   ├── format.sh
│   └── run_static_analysis.sh
├── scripts/                    # 📜 Build/deploy/test/package automation
│   ├── build.sh
│   ├── run_tests.sh
│   └── install.sh
├── .github/                    # 🐙 CI/CD (GitHub Actions)
│   └── workflows/
│       └── build.yml
├── .vscode/                    # 🧠 VSCode settings (optional)
│   ├── settings.json
│   └── tasks.json
├── .gitignore                  # 🙈 Ignore build/ and temp files
├── CMakeLists.txt              # 📐 Top-level CMake
├── Makefile                    # 🧱 Optional alternative to CMake
├── README.md                   # 🏁 Project info, build instructions
├── LICENSE                     # 📄 Project license
└── Doxyfile                    # 📘 Optional Doxygen config
```

### C/C++ Compilation Steps

C and C++ run directly on hardware cpu that's why they are called as compiled languages. All the code is processed into machine code first, before proceeding for execution. C/C++'s speed advantage stems from being a compiled language with minimal overheads. It is considered low level language because of it's ability to interact directly with the hardware like memory etc. The code is highly dependent on the cpu architecture (arm, avr, x86) so binaries are not portable. Often cross compilation is also needed where you compile code for other cpu architecture and generate binaries.

C/C++ are compiled in 4 steps:
- Preprocessing: Inputs source code, resolves preprocessor directives & outputs .i file
- Compilation: Inputs .i file, converts into assembly code and outputs .s file
- Assembly: Inputs .s file, converts into machine code, outputs .o file
- Linking: Resolves dependencies, object code + libraries --> Final Executable

```bash
.c/.cpp file --> Preprocessor --> .i file --> Compilation --> .s file --> Assembly --> .o file --> Linking --> Binary executable
```

### Compilation Commands for C/C++

```bash
# Basic compilation - Single File

gcc main.c -o main
./main

g++ main.cpp -o main
./main



# Basic Compilation - Single file with warnings and c/c++ standard

gcc -Wall -Wextra -std=c17 main.c -o main
./main

g++ -Wall -Wextra -std=c++17 main.cpp -o main
./main



# Compile and link multiple source files

main.c / main.cpp
utils.c / utils.cpp
utils.h

gcc main.c utils.c -o main
./main

g++ main.cpp utils.cpp -o main
./main



# Separately Compile to Object Files, Then Link

gcc -c main.c -o main.o   # generates main.o
gcc -c utils.c -o utils.o  # generates utils.o
gcc main.o utils.o -o main
./main

g++ -c main.cpp -o main.o
g++ -c utils.cpp -o utils.o
g++ main.o utils.o -o main
./main


# Compile with Debugging Information (-g, -g3, -ggdb)

gcc -g main.c -o main
g++ -g main.cpp -o main



# Compile with Optimization - Common levels: -O0, -O1, -O2, -O3, -Ofast

gcc -O2 main.c -o main
g++ -O2 main.cpp -o main


Enabled using -O (capital letter "O", not zero):
-O0: No optimization (default when debugging)
-O1: Some optimization
-O2: Better speed, safe for most programs
-O3: Aggressive optimization — can make your program faster, but may change behavior slightly in rare edge cases
-Os: Optimize for smaller size
-Ofast: Aggressive optimization and ignores some IEEE rules (less safe)





# Cross-compilation for ARM (example)

arm-linux-gnueabi-gcc main.c -o main_arm



# Preprocessing / Assembly / Object / Executable Steps

gcc -E main.c -o main.i     # Preprocessing
gcc -S main.i -o main.s     # Assembly
gcc -c main.s -o main.o     # Object
gcc main.o -o main          # Executable

g++ -E main.cpp -o main.i     # Preprocessing
g++ -S main.i -o main.s     # Assembly
g++ -c main.s -o main.o     # Object
g++ main.o -o main          # Executable
```


```bash
project/
├── src/
│   └── main.c / main.cpp
│   └── utils.c / utils.cpp
├── headers/
│   └── utils.h
├── build/        # <-- object files (.o) go here
├── bin/          # <-- final executable goes here
```

**Scenario: Compilation of multiple files, placed in various directories, target files to be stored in particular directories(refer to project structure above)**

```bash
mkdir -p build # Ensures directory exists: creates one or skips it if exists or else create prehand manually
mkdir -p bin 

gcc -Wall -Wextra -std=c17 -Iheaders -c src/main.c -o build/main.o
gcc -Wall -Wextra -std=c17 -Iheaders -c src/utils.c -o build/utils.o
gcc -Wall -Wextra -std=c17 build/main.o build/utils.o -o bin/myprogram
./bin/myprogram


mkdir -p build # Ensures directory exists: creates one or skips it if exists or else create prehand manually
mkdir -p bin 

g++ -Wall -Wextra -std=c++17 -Iheaders -c src/main.cpp -o build/main.o
g++ -Wall -Wextra -std=c++17 -Iheaders -c src/utils.cpp -o build/utils.o
g++ -Wall -Wextra -std=c++17 build/main.o build/utils.o -o bin/myprogram
./bin/myprogram
```

If you want to prevent the manual hassle of writing so many commands then use make, cmake, cmakelists.txt and makefiles which automate the building process. It's an automation tool very helpful for large c/c++ codebases.



### Other helpful commands list
```bash
which gcc
which clang
which cmake
which make
where gcc
where clang
where cmake
where make
gcc --version
clang --version
cmake --version
make --version
```


### Make command, Makefiles basics

Makefiles are basically meant to automate build process of the source code using automation script. It follows bash scripting syntax as well as has it's own simple syntax. "Make" is a software tool, while "makefile" is a configuration file or lets say a build file.  "Make" uses "makefile" to automate software building and other complex tasks. Makefiles define rules that specify how to build software, including compilation and linking, and are crucial for large projects to streamline the build process and manage dependencies. 

Elaboration:

Make:

Make is a command-line tool that reads instructions from a "makefile". It determines which parts of a project need to be rebuilt based on dependencies and executes the necessary commands.

Makefile:

A makefile is a text file that contains instructions for the "make" tool. It defines the build process, including which files need to be created, what commands to execute, and how dependencies are handled. 

Purpose:

Makefiles are used to automate the building of software projects, especially those with many source files and dependencies. They help ensure that only the necessary parts of a project are rebuilt when changes are made. 

Example:

A simple makefile might define rules for compiling C/C++ code, linking object files into an executable, and running tests. 

Benefits:

Makefiles save time and effort by automating repetitive tasks, reducing errors, and facilitating collaboration on large projects. 

```bash
target: prerequisites
    command
    command
    command
    command
    ...
```

To run it, you just need to type `make` command in terminal and all the contents of the make file will be executed in order. Whenever you enter `make` command in terminal it finds Makefile automatically and searches for keyword `all` unless explicitly specified for example: `make clean` or `make execute` etc for which these specified keywords should exist in the file with as targets, having prerequisites and also commands enlisted underneath.

```bash
make        # By default runs `make all`
make all
make run
make clean
```

An example of a very simple makefile in C would be: with only one code file

```bash
CC = gcc
CFLAGS = -Wall -Wextra -std=c17
SOURCE = src/main.c
TARGET = bin/myprogram
OBJ = build/main.o


all: $(TARGET)

$(TARGET): $(OBJ)
        @mkdir -p bin
        $(CC) $(OBJ) -o $@
        @echo "Executable created"

$(OBJ): $(SOURCE)
        @mkdir -p build
        $(CC) $(CFLAGS) -c $(SOURCE) -o $@
        @echo "Object file created in build/ folder"

clean:
        rm -rf build/*.o $(TARGET)
        @echo "File Cleaning Complete"

run:
        @./bin/myprogram
```

Here `@` prevents printing of the line in terminal. All commands without `@` will be printed on the terminal


For C++, makefile looks as follows:

```bash
CXX = g++
CXXFLAGS = -Wall -Wextra -std=c++20
SOURCE = src/main.cpp
TARGET = bin/myprogram
OBJ = build/main.o


all: $(TARGET)

$(TARGET): $(OBJ)
        @mkdir -p bin
        $(CC) $(OBJ) -o $@
        @echo "Executable created"

$(OBJ): $(SOURCE)
        @mkdir -p build
        $(CC) $(CFLAGS) -c $(SOURCE) -o $@
        @echo "Object file created in build/ folder"

clean:
        rm -rf build/*.o $(TARGET)
        @echo "File Cleaning Complete"

run:
	    @./bin/myprogram
```

You can simplify it even more by writing all commands one under another like this

```bash
CC = gcc
CFLAGS = -Wall -Wextra -std=c17
SOURCE = src/main.c
TARGET = bin/myprogram
OBJ = build/main.o


compile:
        @mkdir -p build
        @mkdir -p bin
        $(CC) $(CFLAGS) -c $(SOURCE) -o $(OBJ)
        $(CC) $(CFLAGS) $(OBJ) -o $(TARGET)


run:
        ./bin/myprogram

clean:
        rm -rf build/*.o $(TARGET)
```

Just run it as
```bash
make compile
make run
make clean
make compile run clean
```

### Concept of CMake, CMakelists.txt & building a binary from source code using cmake


**What is cmake?**

CMake is an open-source, cross-platform build system  generator/tool used to manage the build process of software. It does not directly compile source code but rather generates build files (like `Makefiles` or project files for IDEs) that are then used by other tools to build the software.

- It generates build scripts (like `Makefiles` on Linux or Visual Studio projects on Windows).
- These build scripts then drive tools like `make` or `ninja` to compile your source code into binaries (e.g., executables or libraries).

**What is `CMakeLists.txt`?**

CMakeLists.txt is a configuration txt file used by CMake, a cross-platform build system generator. It acts as an input to CMake and contains a series of commands and instructions that describe how to build a software project, written in CMake's own language. CMake reads these instructions and generates native build files for different platforms, such as Makefiles on Linux and project files for Visual Studio on Windows. his file specifies things like:

- The project's name and version.
- The source files to be compiled.
- The libraries to link against.
- Compiler flags and options.
- The target build system (e.g., Make, Visual Studio, Xcode).

CMake processes CMakeLists.txt files to generate the necessary build files for the chosen platform and compiler. This allows developers to work with a single build system definition while targeting multiple environments.

Example:

```bash
MyProject/
|
|--- main.c
|--- CMakeLists.txt
```

The `CMakeLists.txt` should look like this:

```bash
cmake_minimum_required(VERSION 3.10)        # Minimum CMake version
project(MyProject)                          # Minimum CMake version
add_executable(MyApp main.c)                # Build an executable from main.c
```

The you run:
```bash
cmake .

# OR

mkdir build
cd build
cmake ..        # This reads ../CMakeLists.txt and generates a Makefile

# Then run the `make` command

make            # This compiles the code into the 'MyApp' binary

./MyApp         # Run it!
```

Common `CMakeLists.txt` Elements:

- `cmake_minimum_required(VERSION 3.XX)` : Ensures CMake version compatibility
- `project(MyProjectName VERSION 1.0)`	: Defines the project name and version
- `add_executable(name src1 src2 ...)`	: Builds an executable from source files
- `add_library(name src1 src2 ...)`	: Builds a static/shared library
- `target_include_directories()` : Add include paths
- `target_link_libraries()` : Link with external libraries
- `set(CMAKE_CXX_STANDARD 17)`	: Set C++ standard version


```bash
project/
├── main.cpp
├── utils.cpp
├── utils.h
└── CMakeLists.txt
```

`CMakeLists.txt`:

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

add_executable(MyProject main.cpp utils.cpp)
```

Run these commands on the terminal:
```bash
mkdir build && cd build
cmake ..
make
./MyProject
```

Real world project structure scenario:
```bash
your_project/
├── CMakeLists.txt
├── src/
│   ├── main.c
│   └── utils.c
├── utils/
│   └── utils.h
├── build/
├── bin/
```

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyCProject C)

# Set the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Add compile flags
add_compile_options(-Wall -Wextra -Wpedantic)

# Set output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build)

# Include utils/ folder for headers
include_directories(${CMAKE_SOURCE_DIR}/utils)

# Source files inside src/
set(SOURCES
    src/main.c
    src/utils.c
)

# Create the executable
add_executable(MyApp ${SOURCES})
```

Use `project(MyCProject CXX)` for C++ project


Run the following commands on the terminal:
```bash
mkdir -p build
mkdir -p bin
cd build
cmake ..
make        # Can also use `cmake --build`
./../bin/MyApp



# OR Run this in root project directory

cmake -S . -B build # Configures the build system from your source code
cmake --build build # Compiles and links the code using the generated build files/makefiles in build folder. Baiscally it runs the makefile generated by cmake./

# OR run
make

./bin/myprogram



```

- `cmake ..`	Use parent folder (..) as source dir and current dir as build dir
- `cmake .`	Use current dir as both source and build dir
- `cmake -S X -B Y`	Explicitly specify source and build dirs

When you just type `cmake`, it shows usage instructions because you're not telling it what to do or where the source code is.

CMake needs to know:
- Where the CMakeLists.txt file is (source directory)
- Where to put the build files (build directory)

When you don’t give these, CMake gets confused — hence the help message.


Why `cmake -S . -B build` works? This tells CMake explicitly:

- `-S .` → "Source is in the current folder (.)" — i.e., where CMakeLists.txt is.
- `-B build` → "Put the build output (Makefiles, etc.) in the build/ folder."

So CMake looks at `./CMakeLists.txt`, and generate a build system inside `./build`.




Output directories set inside CMakeLists.txt
```cmake
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build)
```

- These tell where the compiled binary files (executables, static libs, shared libs) go after building.
- For example, executable files get placed in `cpp_practice/bin/`
- Object files, archives, or libraries go into `cpp_practice/build/` folder (or wherever you specify)
- This is unrelated to where CMake puts its build system files — it's about where your final compiled files go.



### Why use Makefile or CMake instead of bash shell script file

Makefiles look a lot like bash scripts, and you could technically build your project with just a shell script. But there are important reasons why Makefiles (and tools like CMake that generate them) exist and are preferred over plain bash scripts. You can, but you lose all the power that make gives you.

For example:

```bash
# build.sh (Bash alternative)
g++ -c src/utils.cpp -o build/utils.o
g++ -c src/main.cpp -o build/main.o
g++ build/main.o build/utils.o -o bin/myprogram
```

This works, but it:
- recompiles everything every time
- doesn't detect what changed
- doesn't do dependency tracking
- doesn't support platform abstraction
- is harder to maintain and scale

Why Makefile is Better. A Makefile + make:
- Tracks dependencies: Only recompiles files that actually changed.
- Has implicit rules: Knows how to compile .cpp to .o or link .o to executable.
- Scales easily: For 10, 50, or 500 source files, you don’t have to write every command manually.
- Cross-platform-ish: You can write makefiles that adapt across Unix-like systems.
- Parallel builds: `make -j4` can build multiple files in parallel automatically.
- Supports phony targets: Like `make clean`, `make test`, etc.
- Run make to build
- Only changed `.cpp/.c` files are recompiled
- Run `make clean` to remove artifacts
- Easy to maintain and extend
- Example in a typical project structure: Each make rule checks timestamps. If main.cpp is newer than main.o, recompile main.cpp. If utils.cpp didn’t change, don’t touch utils.o. If no .cpp file changed, skip compiling altogether
