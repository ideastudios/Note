```xml
repositories {
    flatDir {
        dirs 'libs'
    }
}

        ndk {
            
             abiFilters 'armeabi' 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64', 'mips', 'mips64'
        }
		
		   sourceSets {
            main {
                jniLibs.srcDirs = ['libs']
            }
        }
		
		gradlew  app:dependencies
		
		 compile ('com.***.***:XXX:1.0.0') { // 所加的第三方框架
        exclude group: 'com.android.support', module:'design'     // 加载时排除框架中的design包
 }
		
		
```
