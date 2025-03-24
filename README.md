
IfcOpenShell (3D Repo Fork)
===========================

This is a fork of IfcOpenShell for use by [3drepobouncer](https://github.com/3drepo/3drepobouncer).

It currently tracks 0.8.0.

### Changes (Latest)

None (current fixes are merged upstream)

Problems we are aware of but will not fix:

1. HDF5 caching won't work default materials: https://github.com/IfcOpenShell/IfcOpenShell/issues/6340
2. PropertySetDefinitionSets are not supported: https://github.com/IfcOpenShell/IfcOpenShell/issues/6330
3. [IfcRelDefinesByObject](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/FINAL/HTML/schema/ifckernel/lexical/ifcreldefinesbyobject.htm) does not take the RelatingObject's Representations.


### Building

**Windows v143**

1. Give `set IFCOS_INSTALL_PYTHON=FALSE` before running build-deps.cmd.
2. Make sure to give the build tools with build-deps.cmd, e.g. `build-deps.cmd vs2022-x64`. Despite the samples, this is not optional.
3. Give the same tools for run-cmake.bat, and disable python: `run-cmake.bat vs2022-x64 -DBUILD_IFCPYTHON=0 -DCOLLADA_SUPPORT=0 -DHDF5_SUPPORT=0`


**Windows v142**

1. Give `set IFCOS_INSTALL_PYTHON=FALSE` before running build-deps.cmd
2. Make sure to give the build tools with build-deps.cmd, e.g. `build-deps.cmd vs2019-x64`. Despite the samples, this is not optional.
3. Give the same tools for run-cmake.bat, and disable python: `run-cmake.bat vs2019-x64 -DBUILD_IFCPYTHON=0 -DCOLLADA_SUPPORT=0 -DHDF5_SUPPORT=0`

If receiving linker errors, replace the Boost environment variables with a 3rd party copy of Boost in `run-cmake.bat`, e.g.

```
set BOOST_ROOT=D:\3drepo\bouncer\boost_1_86_0
set BOOST_LIBRARYDIR=D:\3drepo\bouncer\boost_1_86_0\lib64-msvc-14.2
```

The BOOST variables can also be updated in `win/run_cmake.bat`.

IfcOpenShell comes with its own version of OpenCascade (7.8.1).

It is necessary to copy the Eigen dependency into the installed `/include` folder, as `INSTALL` wont do it.

IFCOS 0.7.0 introduced CGAL, which itself introduces two static dependencies. The `FindIFCOPENSHELL` module has been updated to also include these libraries (`mpfr`, `mpir`), however these must be copied into the IfcOpenShell installation `/lib` folder on Windows (on Linux, the CMake will search `usr/libs` which should find the OS versions).
