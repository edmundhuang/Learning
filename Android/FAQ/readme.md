# Frenquently Ask Question

android studio3.0升级问题记录
1. 提示错误 failed to find target with hash string 'android-23'  
打开Android SDK Manager，将对应的SDK版本下载下来即可  

2. android studio3.0升级问题记录
gradle打包，自定义apk名称代码报错（Cannot set the value of read-only property ‘outputFile’ ）   
解决：在app的buide.gradle修改3.0之前输出自定义apk名字的代码，代码如下：  
``` java
//            applicationVariants.all { variant ->
//                variant.outputs.each { output ->
//                    def outputFile = output.outputFile
//                    if (outputFile != null && outputFile.name.endsWith('.apk')) {
//                        def fileName = "小袋快借${defaultConfig.versionName}_${releaseTime()}_${variant.productFlavors[0].name}.apk"
//                        output.outputFile = new File(outputFile.parent, fileName)
//                    }
//                }
//            }
            android.applicationVariants.all { variant ->
                variant.outputs.all {
                    outputFileName = "小袋快借${defaultConfig.versionName}_${releaseTime()}_${variant.productFlavors[0].name}.apk"
                }
            }
```

3. All flavors must now belong to a named flavor dimension. Learn more at https://d.android.com
在主app的build.gradle里面的  
``` java
defaultConfig {
    targetSdkVersion：***
    minSdkVersion ：***
    versionCode：***
    versionName ：***
    //版本名后面添加一句话，意思就是flavor dimension 它的维度就是该版本号，这样维度就是都是统一的了
    flavorDimensions "versionCode"
}
```

4. Unable to resolve dependency for ':app@GooglePlayProductFlavors/compileClasspath': Could not resolve project :libraries:headsupcompat.  

