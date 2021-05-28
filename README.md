# FASTBuild-UE4 Fork
This [FASTBuild](https://github.com/fastbuild/fastbuild) branch is based on v1.04, and modified to fit Unreal 4.26.2, currently only support **windows** platform.

## Features(Modifications)
 1. Replace host name with IP address. [#98a7f04](https://github.com/VicentChen/fastbuild-ue4.26.2/commit/98a7f04af24b0478278b80b68919db0136b46205)
 2. Modify for official `FASTBuild.cs`. [#2252692](https://github.com/VicentChen/fastbuild-ue4.26.2/commit/2252692fc51b1d086a6906516fb526d455bd1e36)
 3. Compress compiled object. [#280d92e](https://github.com/VicentChen/fastbuild-ue4.26.2/commit/280d92e19fce3af4ac86211f73aac317936f7afa)
 4. Support building shaders. [#f99dcc9](https://github.com/VicentChen/fastbuild-ue4.26.2/commit/f99dcc9ce698b92caa788016d72c1c29e18df751)

## Build requirements

 - VS2019 Community 14.28.29910
 - Windows SDK 10.0.19041.0

If different version platform or compiler is used, `.bff` file in `External/SDK` should be modified.

For example, if you are using Windows SDK 10.0.17763.0, version number in `External/SDK/Windows/Windows10SDK.bff` should be modified. If you are using VS2019 Enterprise or a different version, version number in `External/SDK/VisualStudio/VisualStudio.bff` and `External/SDK/VisualStudio/VS2019.bff` should be modified.

## Usage

**Some Notes:**
 - Please use the latest source code in this repo. Commits listed above work only as references for your own modification.
 - Some bugs about FASTBuild cache path frequently happened. Therefore, I hard-coded cache path in `UnrealEngine/ShaderCompilerFASTBuild.cpp` and `UnrealEngine/FASTBuild.cs`. **Please find `F:\\Cache` and modify them to your own cache path.**

### Unreal Engine Source Code Building
 1. Compile this project: run FBuild.exe (official v1.04 release) `FBuild.exe All-x64-Release -dist -clean` in path `Code/`.
 2. Clone `tmp/x64-Release/Tools/FBuild/FBuild/FBuild.exe` and in `tmp/x64-Release/Tools/FBuild/FBuildWorker/FBuildWorker.exe` to `[UnrealEngine Source Code]/Engine/Extras/ThirdPartyNotUE/FASTBuild/Win64`.
 3. (Optional) You may need to modify `FASTBuild.cs`. Please refer to `UnrealEngine/FASTBuild.cs` in this projet.
 4. Done, you can start compiling ue now.

### Unreal Engine Project Building
**Notice that this instruction works for both official Unreal Engine release and your custom build.**
 1. Clone `tmp/x64-Release/Tools/FBuild/FBuild/FBuild.exe` and in `tmp/x64-Release/Tools/FBuild/FBuildWorker/FBuildWorker.exe` to somewhere, and add them to system path.
 2. (Optional) Modify `%APPDATA%/Unreal Engine/UnrealBuildTool/BuildConfiguration.xml`. Please refer to `FASTBuild.cs` and search for `[XmlConfigFile]`.
 3. Done, you can start compiling now.

### Unreal Engine Shaders Building
 1. Compile this project: run FBuild.exe (official v1.04 release) `FBuild.exe All-x64-Release -dist -clean` in path `Code/`.
 2. Clone `tmp/x64-Release/Tools/FBuild/FBuild/FBuild.exe` and in `tmp/x64-Release/Tools/FBuild/FBuildWorker/FBuildWorker.exe` to `[UnrealEngine Source Code]/Engine/Extras/ThirdPartyNotUE/FASTBuild/Win64`.
 3. Clone `UnrealEgine/ShaderCompiler.h, ShaderCompiler.cpp, ShaderCompilerFASTBuild.cpp` to Unreal Engine.
 4. Build Unreal Engine.
 5. **Make sure ALL remotes install DirectX, or you can download [here](https://www.microsoft.com/en-us/download/details.aspx?id=35).**
 5. Done, next time you compile shader, it will automatically start distributed building.

## Issues and Solutions(maybe)
 - **Compilation.** There may be errors about `FileHelper` functions when compiling `ShaderCompilerXGE.cpp` and `ShaderCompilerFASTBuild.cpp`. Add an anonymous namespace, or rename these functions may work.
 - **Timeout.** FASTBuild's author recommends to use 1000M local network but I'm under a 100M one. Therefore it may lead to frequently timeout. Here's my personal experience for this issue(they work for me and hope they work for you too:smile: )
    - If you are using cache, please make sure the cache path is properly written in bff file(or you can try to disable cache).
    - If you are using many core machine, like 28 cores or more, you can try to lower the local compiling thread to 16.
 - **Distributed shader compilation is much more slower than local.** If any remote machine didn't install DirectX, the whole compilation will failed. You need to check `%TEMP%/FASTBuild/FastBuildLog.log` to find which remote is the blacksheep. Then you should [download DirectX from here](https://www.microsoft.com/en-us/download/details.aspx?id=35).
 - **Cache path is not correct.** Please refer to Usage section.

## References
 1. For c++ compile problems: [FASTBuild documentation](https://www.fastbuild.org/docs/documentation.html)
 2. For shader compile problems: [FASTBuild issue 539](https://github.com/fastbuild/fastbuild/issues/539)
