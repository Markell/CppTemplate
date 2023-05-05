# Setup Procedure
1. Download Bash script to create new C++ projects
    ```bash
    curl -O https://raw.githubusercontent.com/TimothyHelton/cpp_project_template/master/new_cpp_project.sh
    chmod u+x new_cpp_project.sh
    ```
1. Create new C++ project
    ```bash
    ./new_cpp_project.sh NewProjectName
    ```
1. In the project top level **CMakeLists.txt**:
    1. Line 2: Change the variable **MyProject** to the name of your project.
        ```cmake
        project(NewProject)
        ```
        - This variable will be used in a couple of different places.
            - MyProject_run: will be the main executable name
            - MyProject_lib: will be the project library name
    1. Line 4: Set the version of C++ to use.  For example, let's set up the
       NewProject to use C++ 11.
        ```cmake
        set(CMAKE_CXX_STANDARD 11)
        ```
1. Update project name and description in the `Doxyfile` located in the `docs`
   directory.
    1. Update line `PROJECT_NAME`
        1. This name will appear on each documentation page.
    1. Update line `PROJECT_NUMBER`
        1. This is the version number of your project.
    1. Update line `PROJECT_BRIEF`
        1. Any text entered here will also appear on each documentation page.
           Try not to make this one too long.
1. Reload the top CMake file.

## CLION IDE Specific Instructions
I started using an IDE from [JET Brains](https://www.jetbrains.com/) tailored
for Python called [PyCharm](https://www.jetbrains.com/pycharm/) and thought
it helped me write better code.
I'd been wanting to learn C++ and decided to give JET Brains C/C++ IDE called
[CLion](https://www.jetbrains.com/clion/) a try.
The code completion, interactive suggestions, debugger, introspection tools,
and built-in test execution are very handy.
There are a couple extra details to set when using this IDE.

1. The IDE allows you to mark directories with their desired purpose.
   To mark a directory right click on the directory name in the `Project` window
   and select `Mark Directory as` from the drop-down menu.
    1. Mark the `src` directory as `Project Sources and Headers`
    1. Mark the `tests/lib/googletest` directory as  `Library Files`
1. Setup the `Run/Debug Configuration` by selecting `Edit Configurations...`
   from the pull-down menu from the run button (green triangle) in the upper right
   corner.
    1. Update Doxygen Build to execute the unit test suite.
        1. Select Doxygen from the Application menu on the left.
        1. Choose the **executable** for Doxygen to be `Unit_Tests_run`.
    1. Create a `Google Test` configuration
        1. In the upper left corner select the plus symbol.
        1. Chose `Google Test` from the drop-down menu.
        1. Set **Name** to `Unit Tests`.
        1. Set **Target** to `Unit_Tests_run`.

## Doxygen - Documentation Setup
Skip this if you already have doxygen configured
* Install `doxygen`
    * macOS - `brew install doxygen`
    * Ubuntu - `sudo apt-get install -y doxygen`
* Create doxygen config file (Doxyfile). Run `doxygen -g`
* Configure `Doxyfile`
    * Set `RECURSIVE` to `YES`
    * Set `EXCLUDE` and `EXCLUDE_PATTERNS` to exclude directories you don't want documented. Typically library code and plugins come here.
    * Set `PROJECT_NAME` to the name of your project
* Optionally add `html` and `latex` to `.gitignore` file
* Document your code according to Doxygen guidlines
    * Check `src/main.c` for C style documentation. Output can be seen [here](https://satu0king.github.io/Github-Documentation-With-Doxygen/main_8c.html).
    * Check `src/main.cpp` for C++ style documentation. Output can be seen [here](https://satu0king.github.io/Github-Documentation-With-Doxygen/main_8cpp.html)
    * Check `src/main.py` for Python style documentation. Output can be seen [here](https://satu0king.github.io/Github-Documentation-With-Doxygen/namespacemain.html)
* Optionally run `doxygen` to generate documentation to see output documentation locally
    * By default web documentation and pdf documentation files are generated in `html` and `latex` directories respectively.
    * View web documentation at `html/index.html`
    * Compile pdf documentation by running `make` in `latex` directory
    * Class list can be seen [here](https://satu0king.github.io/Github-Documentation-With-Doxygen/annotated.html)

## Configuring automatic publishing using github actions
* Copy the action file `main.yml` to `.github/workflows/main.yml`
* Commit and Push to github
* Github action should automatically start running
* Confirm that github is set to deploy `gh-pages` branch in settings page

## Notes
* Ensure that `publish_dir` in `main.yml` is set correctly