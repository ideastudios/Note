# Mac 环境变量配置

## .bash_profile 配置
```
# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"
export PATH
export ANDROID_HOME=/Users/lx/Library/Android/sdk
export NDK_HOME=/Users/lx/Library/Android/sdk/ndk-bundle
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$NDK_HOME

export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_201.jdk/Contents/Home
export JRE_HOME=$JAVA_HOME/jre
export PATH=$PATH:$JAVA_HOME/bin

export CLASSPATH=$JAVA_HOME/lib/toosl.jar:$JAVA_HOME/lib/dt.jar
export CLASSPATH

```