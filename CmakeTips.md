# Cmake tips
Copilot with modification, 20241128

## Using Graphviz to visualize structure
### Generate a Graphviz File:
Navigate to your project’s build directory.
Run the following command to generate a Graphviz dot file representing your project’s dependencies:
```bash
cmake --graphviz=cmakedep.dot ../
```
This command will create a cmakedep.dot file containing a textual description of your project’s dependency graph

### Visualize the Graph:
Use a Graphviz tool (like dot) to convert the .dot file into a visual format (e.g., PNG, PDF)
```bash
dot -Tpng cmakedep.dot -o cmakedep.png
```
Open cmakedep.png

## Use the cmake presets to configure, build and test a project
Open your terminal and navigate to your project directory.
Run the following commands to configure the project using the preset.
### - prepare:
Open your terminal and navigate to your project directory.
Clear a build directory:
```bash
rm -rf build
```
### - configure:
```bash
cmake --preset <your-preset-name>
```
### - build:
```bash
cmake --build --preset <your-preset-name>
```
### - test:
```bash
ctest --preset <your-preset-name>
```
### - to run all at once, use workflow:
```bash
cmake --workflow --preset <your-preset-name>
```
## To use a common way to configure, build and test a project with Ninja
### - prepare the Project:
Open your terminal and navigate to your project directory.
Create a build directory and navigate into it:
```bash
mkdir build
cd build
```
or clear the build directory
### - run the following command in the build directory to configure a project:
```bash
cmake .. -G Ninja
```
### - build a project in the build directory:
```bash
cmake --build .
```
### - run tests in the build directory:
```bash
ctest
```
