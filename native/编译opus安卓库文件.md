# OPUS安卓版

## 下载 http://www.opus-codec.org/downloads/

## 步骤 

+ 下载后解压 配置NDK 将NDK加入path中
+ 新建文件夹out(栗子) 然后在文件夹中新建两个文件  Android.mk Application.mk

其中 Android.mk
```
LOCAL_PATH := $(call my-dir)/..

include $(CLEAR_VARS)


include $(LOCAL_PATH)/celt_sources.mk
include $(LOCAL_PATH)/silk_sources.mk
include $(LOCAL_PATH)/opus_sources.mk

# 输出的文件名称 libopus.so
LOCAL_MODULE        := opus

SILK_SOURCES        += $(SILK_SOURCES_FIXED)
CELT_SOURCES        += $(CELT_SOURCES_ARM)
SILK_SOURCES        += $(SILK_SOURCES_ARM)

# 指定源码文件
LOCAL_SRC_FILES     := \
    $(CELT_SOURCES) $(SILK_SOURCES) $(OPUS_SOURCES) $(OPUS_SOURCES_FLOAT)

LOCAL_LDLIBS        := -lm -llog
LOCAL_C_INCLUDES    := \
    $(LOCAL_PATH)/include \
    $(LOCAL_PATH)/silk \
    $(LOCAL_PATH)/silk/fixed \
    $(LOCAL_PATH)/celt

# 编译参数配置
LOCAL_CFLAGS        := -DNULL=0 -DSOCKLEN_T=socklen_t -DLOCALE_NOT_USED -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64
LOCAL_CFLAGS        += -Drestrict='' -D__EMX__ -DOPUS_BUILD -DFIXED_POINT -DUSE_ALLOCA -DHAVE_LRINT -DHAVE_LRINTF -O3 -fno-math-errno
LOCAL_CPPFLAGS      := -DBSD=1 
LOCAL_CPPFLAGS      += -ffast-math -O3 -funroll-loops

include $(BUILD_SHARED_LIBRARY)
```

Application.mk
```
APP_STL := stlport_shared
APP_ABI := all
APP_PLATFORM := android-19
NDK_TOOLCHAIN_VERSION := 4.9
APP_CPPFLAGS += -Wno-error=format-security
```
+ 打开命令行进入out(栗子) 输入ndk-build NDK_PROJECT_PATH=. NDK_APPLICATION_MK=Application.mk APP_BUILD_SCRIPT=Android.mk