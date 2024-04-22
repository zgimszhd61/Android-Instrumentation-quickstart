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
