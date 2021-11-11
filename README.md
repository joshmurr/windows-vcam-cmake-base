# Directshow VCam with CMake

This is the basic [tmhare.mvps.org-vcam](https://github.com/roman380/tmhare.mvps.org-vcam) setup, but found the process of downloading the _Windows Classic Samples_ and editing the `.props` file a bit fiddly, so the _Baseclasses_ and `strmbase.lib` are included here.

### Build Instruction

```bash
mkdir build && cd build
cmake ..
```

Then open `vcam.sln` and build from Visual Studio. Then you'll need to register the DLL in `/build/src/{TARGET}/virtual-cam.dll` using Powershell or something (with admin privileges):

```bash
regsvr32 /path/to/virtual-cam.dll
```
