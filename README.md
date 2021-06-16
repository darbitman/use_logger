# consume the logger package
First
```
mkdir build
```
then
```
cd build
```
Make sure the package was created locally. See https://github.com/darbitman/logger to create the package.
Then inside `build`,
```
conan install ..
```
This will create the required cmake files to use the logger package.
Then follow the typical process to use cmake to generate build files and then build.