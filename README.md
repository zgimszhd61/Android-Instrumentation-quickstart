# Android-Instrumentation-quickstart
要在Android应用中进行运行时代码插桩并插入一个简单的 "Hello World" 示例，您可以使用Android的Instrumentation框架。以下是一个快速入门示例，展示如何在Android应用中设置和运行一个基本的Instrumentation测试，以输出 "Hello World"。

### 步骤 1: 创建新的Android项目

首先，您需要在Android Studio中创建一个新的Android项目。

### 步骤 2: 添加测试依赖

在项目的 `build.gradle` 文件中，添加必要的测试依赖。这通常包括JUnit和Android测试库。

```gradle
dependencies {
    // JUnit4 framework
    testImplementation 'junit:junit:4.13.2'
    // AndroidX Test - Instrumentation API
    androidTestImplementation 'androidx.test:runner:1.4.0'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
}
```

### 步骤 3: 编写Instrumentation测试类

在 `src/androidTest/java/` 目录下创建一个新的测试类。例如，您可以创建一个名为 `ExampleInstrumentedTest` 的类。

```java
import androidx.test.platform.app.InstrumentationRegistry;
import androidx.test.ext.junit.runners.AndroidJUnit4;

import org.junit.Test;
import org.junit.runner.RunWith;

import static org.junit.Assert.*;

/**
 * Instrumented test, which will execute on an Android device.
 */
@RunWith(AndroidJUnit4.class)
public class ExampleInstrumentedTest {
    @Test
    public void useAppContext() {
        // Context of the app under test.
        Context appContext = InstrumentationRegistry.getInstrumentation().getTargetContext();
        assertEquals("com.example.myapp", appContext.getPackageName());
        System.out.println("Hello World");
    }
}
```

在这个测试中，我们使用 `InstrumentationRegistry.getInstrumentation().getTargetContext()` 来获取应用的上下文，并验证它的包名。此外，我们在控制台输出 "Hello World"。

### 步骤 4: 运行测试

在Android Studio中，您可以直接运行这个测试。右键点击测试类或方法，选择 "Run"，然后选择您的测试方法。确保您有一个连接的Android设备或已启动的Android模拟器。

这个简单的例子展示了如何在Android项目中设置和运行Instrumentation测试。通过这种方式，您可以在运行时对应用进行插桩，进而进行更复杂的操作和验证。

Citations:
[1] https://developer.android.com/guide/topics/manifest/instrumentation-element
[2] https://mas.owasp.org/MASTG/techniques/generic/MASTG-TECH-0051/
[3] https://source.android.com/docs/core/runtime
[4] https://docs.appdynamics.com/appd/23.x/latest/en/end-user-monitoring/mobile-real-user-monitoring/instrument-android-applications/customize-the-android-build/enable-disable-instrumentation-for-build-types
[5] https://developer.android.com/topic/performance/benchmarking/microbenchmark-write
[6] https://notwoods.github.io/mockk-guidebook/docs/quick/android/
[7] https://source.android.com/docs/core/tests/development/instrumentation
[8] https://developer.android.com/reference/android/app/Instrumentation
[9] https://www.youtube.com/watch?v=bbMsuI2p1DQ
[10] https://developer.android.com/guide
[11] https://developer.android.com/topic/performance/tracing
[12] https://developer.android.com/training/dependency-injection
[13] https://perfetto.dev/docs/quickstart/callstack-sampling
[14] https://perfetto.dev/docs/quickstart/android-tracing
[15] https://developer.android.com/training/testing/instrumented-tests
[16] https://www.geeksforgeeks.org/dagger-hilt-in-android-with-example/
[17] https://developer.android.com/training/dependency-injection/hilt-android
[18] https://stackoverflow.com/questions/4325639/android-calling-javascript-functions-in-webview
[19] https://github.com/i-love-flamingo/example-helloworld
[20] https://www.simplilearn.com/tutorials/angular-tutorial/angular-hello-world

-----

在使用Kotlin语言编写的Android应用中进行运行时代码插桩通常涉及到使用字节码操作库，如ASM，来修改编译后的字节码。以下是一个简单的示例，展示如何在一个使用Kotlin编写的Android应用中插入"Hello World"日志输出，以及如何设置项目以支持这种插桩。

### 步骤 1: 创建一个新的Android项目

首先，你需要在Android Studio中创建一个新的Android项目。选择Kotlin作为项目的编程语言。

### 步骤 2: 添加ASM库依赖

在项目的`build.gradle`文件中添加ASM库的依赖，以便进行字节码操作。你可以添加如下依赖：

```gradle
dependencies {
    implementation 'org.ow2.asm:asm:9.1'
    implementation 'org.ow2.asm:asm-util:9.1'
    implementation 'org.ow2.asm:asm-commons:9.1'
}
```

### 步骤 3: 创建一个Gradle插件进行插桩

在`buildSrc`目录下创建一个新的Gradle插件。如果你的项目中没有`buildSrc`目录，你需要先创建它。这个目录允许你编写并包含自定义的Gradle逻辑。

在`buildSrc`中，创建以下文件结构：

```
buildSrc/
└── src/
    └── main/
        ├── groovy/
        │   └── MyPlugin.groovy
        └── resources/
            └── META-INF/
                └── gradle-plugins/
                    └── myplugin.properties
```

在`MyPlugin.groovy`文件中，编写一个简单的插件，使用ASM来修改字节码：

```groovy
import org.gradle.api.Plugin
import org.gradle.api.Project
import com.android.build.gradle.AppExtension
import org.gradle.api.tasks.compile.JavaCompile

class MyPlugin implements Plugin<Project> {
    void apply(Project project) {
        project.afterEvaluate {
            AppExtension android = project.extensions.findByType(AppExtension)
            android.applicationVariants.all { variant ->
                JavaCompile javaCompile = variant.javaCompileProvider.get()
                javaCompile.doLast {
                    // 这里添加ASM代码操作字节码
                    println("Hello World from ASM!")
                }
            }
        }
    }
}
```

在`myplugin.properties`文件中，指定插件的实现类：

```
implementation-class=MyPlugin
```

### 步骤 4: 应用你的Gradle插件

在项目的`build.gradle`文件中应用你刚刚创建的插件：

```gradle
plugins {
    id 'myplugin'
}
```

### 步骤 5: 运行你的应用

现在，当你构建并运行你的应用时，ASM插件将会在编译过程中输出"Hello World"，表示插桩已经被执行。

这个示例展示了如何设置一个简单的运行时代码插桩环境。在实际应用中，你可能需要编写更复杂的ASM代码来修改特定的方法或类的字节码。

Citations:
[1] https://juejin.cn/post/6844904185633177608
[2] https://developer.android.com/samples
[3] https://blog.csdn.net/whjk20/article/details/126606348
[4] https://blog.csdn.net/maniuT/article/details/134077405
[5] https://www.cnblogs.com/xiaowenshu/p/10382177.html
[6] https://juejin.cn/post/7284143489737719848
[7] https://juejin.cn/post/7089328997598756894
[8] https://juejin.cn/post/7182178552207376421
[9] https://blog.yorek.xyz/android/paid/master/bytecode/
[10] https://www.volcengine.com/theme/6597249-S-7-1
[11] https://cloud.tencent.com/developer/article/1651227
[12] https://www.volcengine.com/theme/3861483-D-7-1
[13] https://juejin.cn/post/7079229035254906888
[14] https://pytorch.org/mobile/android/
[15] https://blog.csdn.net/aidijava/article/details/136047378
[16] https://blog.csdn.net/weixin_40425640/article/details/127770453
[17] https://developer.aliyun.com/article/175942
[18] https://developer.aliyun.com/article/864244
[19] https://blog.csdn.net/leven98/article/details/123354865
[20] https://developer.aliyun.com/article/864197


