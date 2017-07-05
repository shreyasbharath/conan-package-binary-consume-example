# Prerequisites
Note that this example assumes that you have already uploaded [this](https://github.com/shreyasbharath/conan-package-binary-example) package to a Conan remote.
If you haven't, please follow the instructions on that repo to create and upload the package first.

# Consuming Uploaded Package
`install_deps.py`
This executes the `conan install . -g txt`, which installs the Test package that was uploaded previously to local project directory.

`conanfile.txt`
 The `[imports]` section below instructs Conan to extract the contents of the downloaded package into your local project directory. Specifically, it extracts all .h and .a files from the package and puts them into `include` and `lib` directories respectively.
 
    [requires]
    Test/0.1@myuser/testing

    [generators]
    txt

    [imports]
    include, *.h -> ./include # Copies all header files from packages include folders to my "include" folder
    lib, *.a -> ./lib         # Copies all static libraries from packages lib folders to my "lib" folder
    
## Integrating Into Client's Build Process
Once the package has been extracted, it's up to the client to incorporate those newly created directories into its build process. For example, the `include` directory can be added to the compile options for the compiler and the `lib` directory to the link options for the linker.

# Credits
A big thanks to @memsharded and @drodri for their help.
