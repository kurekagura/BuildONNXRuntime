# onnxruntimeのビルド

[Build ONNX Runtime from source](https://onnxruntime.ai/docs/build/)

## 環境

「Developer Command Prompt for VS 2022」を利用した

```cmd
>systeminfo |findstr /B /C:"OS Name" /B /C:"OS"
OS 名:                  Microsoft Windows 11 Pro
OS バージョン:          10.0.22631 N/A ビルド 22631
```

```cmd
>where nvcc && where nvvp
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.6\bin\nvcc.exe
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.6\bin\nvvp.bat
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.6\libnvvp\nvvp.exe
```

```cmd
>nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2024 NVIDIA Corporation
Built on Thu_Sep_12_02:55:00_Pacific_Daylight_Time_2024
Cuda compilation tools, release 12.6, V12.6.77
Build cuda_12.6.r12.6/compiler.34841621_0
```

```cmd
>where cmake && cmake --version
C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\CMake\bin\cmake.execmake version 3.28.3-msvc11
CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

```cmd
>python -V
Python 3.11.9
```

## Build

### DirectMLビルド

```cmd
git clone <https://github.com/microsoft/onnxruntime.git>
cd onnxruntime
git checkout v1.13.1

build.bat --cmake_extra_defines CMAKE_SYSTEM_NAME=Windows CMAKE_SYSTEM_PROCESSOR=x86_64 --config Release --parallel --update --build --build_shared_lib --use_dml --enable_wcos --use_winml
```

※ --use_cudaではないので、CUDAは不要かもしれません。

ビルド生成物 : microsoft\onnxruntime\build\Windows\Release\Release

- DirectML.dll
- onnxruntime.dll

## 参考・深謝

- [VOICEVOX用にONNXRuntime（DirectML）を改造してGPUを選択できるようにしたい](https://qiita.com/kmatsumoto630823/items/59841ef95e59358d5ab5)

- [onnxruntime ビルド手順](https://zenn.dev/uint256_t/scraps/7055f7719cb60a)
