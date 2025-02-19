# Refresh UE C++ Project
Rebuild C++ without having to delete intermediary and .vs. Set the UE_5.3 to the engine version you use's build tool.

``` bat
@echo off

for %%i in (*.uproject) do set UProjectAbsolutePath=%cd%\%%i
popd
set EnginePath=C:\Program Files\Epic Games\UE_5.3\Engine\Binaries\DotNET\UnrealBuildTool\UnrealBuildTool.exe

echo UProjectAbsolutePath is: %UProjectAbsolutePath%
echo EnginePath is: %EnginePath%

"%EnginePath%" -projectfiles -project="%UProjectAbsolutePath%" -game -rocket -progress

pause
```

I like to keep commands like this in a scripts folder in my project dir so in my custom version i include a "pushd ..\" to move back a directory:

``` bat
@echo off

pushd ..\
for %%i in (*.uproject) do set UProjectAbsolutePath=%cd%\%%i
popd
set EnginePath=C:\Program Files\Epic Games\UE_5.3\Engine\Binaries\DotNET\UnrealBuildTool\UnrealBuildTool.exe

echo UProjectAbsolutePath is: %UProjectAbsolutePath%
echo EnginePath is: %EnginePath%

"%EnginePath%" -projectfiles -project="%UProjectAbsolutePath%" -game -rocket -progress

pause
```