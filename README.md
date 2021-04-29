# FASTBuild-UE4 Fork
This FASTBuild branch is based on v1.04, and modified to fit Unreal 4.26.2, currently only support **windows** platform.

## Modification
 1. Replace host name with IP address.
 2. Modify to make official `FASTBuild.cs` happy.
 3. Compress compiled object.

## Build requirements
 - VS2019 Community 14.28.29910
 - Windows SDK 10.0.19041.0

If different version platform or compiler is used, `.bff` file in `External/SDK` should be modified.

For example, if you are using Windows SDK 10.0.17763.0, version number in `External/SDK/Windows/Windows10SDK.bff` should be modified. If you are using VS2019 Enterprise or a different version, version number in `External/SDK/VisualStudio/VisualStudio.bff` and `External/SDK/VisualStudio/VS2019.bff` should be modified.

## Usage
 1. Compile this project: run FBuild.exe (official v1.04 release) `FBuild.exe All-x64-Release -dist -clean` in path `Code/`.
 2. Clone `FBuild.exe` in `tmp/x64-Release/Tools/FBuild/FBuild` and `FBuildWorker.exe` in `tmp/x64-Release/Tools/FBuild/FBuildWorker` to `[UnrealEngine Source Code]/Engine/Extras/ThirdPartyNotUE/FASTBuild/Win64`.
 3. Done, you can start compiling ue now.

# FASTBuild (v1.04)

FASTBuild is a build system for Windows, OSX and Linux, supporting distributed compilation and object caching. It is used by many game developers, from small independent teams to some of the largest studios in the world.

FASTBuild's focus is on fast compile times in both full build and local iteration scenarios.

A large variety of compilers and target architectures are supported. More details, including hosted documentation and Binary downloads can
be found here: http://fastbuild.org

## Branch policy

**Patches will only be accepted into the "dev" branch.**

| Branch | Status | Purpose |
| :----- | :----- | :----- |
| master | [![Build Status](https://travis-ci.com/fastbuild/fastbuild.svg?branch=master)](https://travis-ci.com/fastbuild/fastbuild) | Stable branch containing snapshot of latest release |
| dev    | [![Build Status](https://travis-ci.com/fastbuild/fastbuild.svg?branch=dev)](https://travis-ci.com/fastbuild/fastbuild) | Development branch for integration of pull requests |

## Contribution Guidelines

Improvements and bug fixes are gladly accepted. FASTBuild has been improved immensely by the contributions of many users. To help facilitate ease of integration, please:

**Constrain pull requests to individual changes where possible** - Simple changes are more easily integrated and tested. Pull requests with many changes, where there are issues with one change in particular, will delay the integration of all changes. Pull requests that change or add large amounts of functionality are harder to test and will take much longer to integrate, increasing the likelyhood of conflicts.

**Avoid refactoring and formatting changes mixed with functional changes** - Behavior altering changes (fixes, enhancements and new features) mixed with style changes or refactoring cleanup make changes more difficult to integrate. Please consider splitting these changes so they can more easily be individually integrated.

**Update and extend tests if appropriate** - There are a large set of unit and functional tests. Please update or add new tests if appropriate.

**Update documentation if appropriate** - For changes in behaviour, or addition of new features, please update the documentation.

**Adhere to the coding style** - Please keep variable/function naming, whitespace style and indentation (4 space tabs) consistent. Consistency helps keep the code maintainable.
