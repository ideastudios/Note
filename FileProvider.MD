FileProvider

## FileProvider是一个特殊的继承自ContentProvider的子类，它通过创建content:// Uri 而不是创建 file:/// Uri的方式，安全地和与之相关的应用进行文件的分享.
1. content:// Uri允许临时访问权限、读写访问权限 通过创建Intent时传入，或者setFlags()的方式
2. file:/// Uri的方式必须修改底层文件的文件系统权限，其他任何应用也可以使用时，不安全

## 定义FileProvider
```xml
<manifest>
    ...
    <application>
        ...
        <provider
            android:name="android.support.v4.content.FileProvider"
            android:authorities="com.mydomain.fileprovider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths" />
        </provider>
        ...
    </application>
</manifest>
```

## 指定可用文件

```xml
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <files-path name="my_images" path="images/"/>
    ...
</paths>
```
paths元素可以包含以下一个或多个元素
1. <files-path name="name" path="path" /> 根目录相当于应用程序内部存储区域的子目录中的文件Context.getFilesDir()
2. <cache-path name="name" path="path" /> 根目录相当于应用程序内部存储区域的缓存子目录中的文件Context.getCacheDir()
3. <external-path name="name" path="path" /> 根目录相当于外部存储区域根目录中的文件Environment.getExternalStorageDirectory()
4. <external-files-path name="name" path="path" />根目录相当于应用程序外部存储区域根目录中的文件Context.getExternalFilesDir(String) Context.getExternalFilesDir(null)
5. <external-cache-path name="name" path="path" /> 根目录相当于应用程序外部缓存区域根目录中的文件Context.getExternalCacheDir()
6. <external-media-path name="name" path="path" /> 根目录相当于应用外部媒体区域根目录中的文件Context.getExternalMediaDirs() API 21+
7. 以上元素都包含两个属性，其中name属性为URI路径 path属性为实际的子目录（只能是目录，不能为单个文件）
8. 文件路径为res/xml/file_paths.xml 在provider标签添加meta-data标签 "android：name”属性设置为 android.support.FILE_PROVIDER_PATHS, "android：resource"属性设置为@xml/file_paths

## 生成文件的Content URI
1. 要使用内容URI与其他应用共享文件，您的应用必须生成内容URI
2. 生成URI 创建File 调用getUriForFile() 
3. 可以通过Intent将URI发送给另一个app
4. 接收内容URI的客户端应用可以打开文件并通过调用ContentResolver.openFileDescriptorget来访问其内容 ParcelFileDescriptor

+ 举个栗子，假设你想通过FileProvider提供文件，获取URI的方式为
```java
File imagePath = new File(Context.getFilesDir(), "images");//私有文件目录
File newFile = new File(imagePath, "default_image.jpg");//文件
Uri contentUri = getUriForFile(getContext(), "com.mydomain.fileprovider", newFile);
```
+ 通过上面代码 defau_image.jpg的content URI为 content://com.mydomain.fileprovider/my_images/default_image.jpg

## 授予URI临时权限
+ Context.grantUriPermission(package, Uri, mode_flags) FLAG_GRANT_READ_URI_PERMISSION FLAG_GRANT_WRITE_URI_PERMISSION 或者两者 权限保持有效直到revokeUriPermission()

## 向另一个应用程序提供内容URI


