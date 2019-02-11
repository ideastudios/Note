```xml
apply plugin: 'com.android.application'

apply plugin: 'kotlin-android'

apply plugin: 'kotlin-android-extensions'

android {

    compileSdkVersion 28
    defaultConfig {
        applicationId "cn.com.pingan.paai.camerandphoto"
        minSdkVersion rootProject.ext.appMinSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode rootProject.ext.versionCode
        versionName rootProject.ext.versionName
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"


        externalNativeBuild {
            cmake {
                cppFlags ""
//                path "CMakeLists.txt"
            }
        }
        ndk {

            abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64', 'mips', 'mips64'
        }
    }

    signingConfigs {
        debugConfig {
            keyAlias 'paaivoice'
            keyPassword 'biggerthanbigger'
            storeFile file('release.jks')
            storePassword 'biggerthanbigger'
        }
        release {
            keyAlias 'paaivoice'
            keyPassword 'biggerthanbigger'
            storeFile file('release.jks')
            storePassword 'biggerthanbigger'
        }
    }



    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }

        packagingOptions {
            exclude 'META-INF/DEPENDENCIES'
            exclude 'META-INF/NOTICE'
            exclude 'META-INF/LICENSE'
            doNotStrip '*/mips/*.so'
            doNotStrip '*/mips64/*.so'
        }
    }


    //文件映射关系
    sourceSets.main {
        jni.srcDirs = ['jniLibs']//nativie文件的目录
    }

    repositories {
        flatDir {
            dirs 'libs'
        }
    }

//    task nativeLibsToJar(type: Zip, description: "create a jar archive of the native libs") {
//        destinationDir file("$projectDir/libs")
//        baseName "Native_Libs2"
//        extension "jar"
//        from fileTree(dir: "libs", include: "**/*.so")
//        into "lib"
//    }
//    tasks.withType(JavaCompile) {
//        compileTask -> compileTask.dependsOn(nativeLibsToJar)
//    }

}
//获取当前时间
def getCurrentTime() {
    return new Date().format("yyyy-MM-dd", TimeZone.getTimeZone("UTC"))
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    implementation "com.android.support:appcompat-v7:$rootProject.ext.supportVersion"
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
    implementation("com.zhihu.android:matisse:0.5.2-beta4") {
        exclude group: 'com.android.support'
        exclude group: 'com.android.support', module: 'design'
//        命令行执行:gradlew  app:dependencies 查看依赖树
    }
}
	
	ext{
    // Sdk and tools
    minSdkVersion = 15
    targetSdkVersion = 26
    compileSdkVersion = 26
    buildToolsVersion = '25.0.2'
 
    // App dependencies
    junitVersion = '4.12'
    v7Version='26.1.0'
}
	
```
