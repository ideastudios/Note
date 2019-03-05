# 库工程中加入C代码和SO文件

## 文件结构

```

library/libs/x86_64/libopus.so
library/libs/x86/libopus.so
library/libs/armeabi-v7a/libopus.so
library/libs/arm64-v8a/libopus.so  表示根据不同CPU类型的已经编译好的so文件

library/src/main/jni/opus.h
library/src/main/jni/opus_custom.h
library/src/main/jni/opus_defines.h
library/src/main/jni/opus_multistream.h
library/src/main/jni/opus_projection.h
library/src/main/jni/opus_types.h
library/src/main/jni/OpusDecoder.cpp
library/src/main/jni/OpusDecoder.h

其中 前6个为 opus的头文件 后两个文件为自定义的头文件和cpp文件

```

CMakeLists.txt
```
cmake_minimum_required(VERSION 3.4.1)

add_library(libopus
        SHARED
        IMPORTED)
set_target_properties(libopus
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libopus.so)

add_library( # 将指定的源文件生成链接文件，然后添加到工程中去
        native-lib

        SHARED

        src/main/jni/OpusDecoder.cpp
        src/main/jni/OpusDecoder.h)

find_library(
        log-lib
        log)


target_link_libraries( # 将目标文件与库文件进行链接
        native-lib
		
        libopus
        

        # included in the NDK.
        ${log-lib})
		
```