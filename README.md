## Compose on stable AGP

### Experiments

<table>
<tr><td>Configuration</td><td>Result</td></tr>
<tr>
<td>

```groovy
android {
    // ...

    buildFeatures {
        compose true
    }
    composeOptions {
        kotlinCompilerExtensionVersion compose_version
        kotlinCompilerVersion '1.4.10'
    }
}
```

</td>
<td>

```
> Task :app:prepareDebugKotlinCompileTask FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:prepareDebugKotlinCompileTask'.
> Could not resolve all files for configuration ':app:kotlin-extension'.
   > Could not find androidx.compose:compose-compiler:1.0.0-alpha06.
     Searched in the following locations:
       - https://dl.google.com/dl/android/maven2/androidx/compose/compose-compiler/1.0.0-alpha06/compose-compiler-1.0.0-alpha06.pom
       - https://jcenter.bintray.com/androidx/compose/compose-compiler/1.0.0-alpha06/compose-compiler-1.0.0-alpha06.pom
     Required by:
         project :app

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org
```

</td>
</tr>
<tr>
<td>

```groovy
android {
    // ...

    buildFeatures {
        compose true
    }
    composeOptions {
        // kotlinCompilerExtensionVersion compose_version
        kotlinCompilerVersion '1.4.10'
    }
}
```

</td>
<td>

```
java.lang.AbstractMethodError: Receiver class androidx.compose.plugins.kotlin.ComposeIrGenerationExtension does not define or inherit an implementation of the resolved method 'abstract void generate(org.jetbrains.kotlin.ir.declarations.IrModuleFragment, org.jetbrains.kotlin.backend.common.extensions.IrPluginContext)' of interface org.jetbrains.kotlin.backend.common.extensions.IrGenerationExtension.
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade$doGenerateFiles$1.invoke(JvmBackendFacade.kt:72)
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade$doGenerateFiles$1.invoke(JvmBackendFacade.kt:34)
	at org.jetbrains.kotlin.psi2ir.Psi2IrTranslator.generateModuleFragment(Psi2IrTranslator.kt:98)
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade.doGenerateFiles(JvmBackendFacade.kt:87)
	at org.jetbrains.kotlin.backend.jvm.JvmIrCodegenFactory.generateModule(JvmIrCodegenFactory.kt:40)
	at org.jetbrains.kotlin.codegen.KotlinCodegenFacade.compileCorrectFiles(KotlinCodegenFacade.java:35)
	at org.jetbrains.kotlin.cli.jvm.compiler.KotlinToJVMBytecodeCompiler.generate(KotlinToJVMBytecodeCompiler.kt:616)
	at org.jetbrains.kotlin.cli.jvm.compiler.KotlinToJVMBytecodeCompiler.compileModules$cli(KotlinToJVMBytecodeCompiler.kt:203)
	at org.jetbrains.kotlin.cli.jvm.K2JVMCompiler.doExecute(K2JVMCompiler.kt:164)
	at org.jetbrains.kotlin.cli.jvm.K2JVMCompiler.doExecute(K2JVMCompiler.kt:51)
	at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.kt:86)
	at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.kt:44)
	at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:98)
	at org.jetbrains.kotlin.incremental.IncrementalJvmCompilerRunner.runCompiler(IncrementalJvmCompilerRunner.kt:346)
	at org.jetbrains.kotlin.incremental.IncrementalJvmCompilerRunner.runCompiler(IncrementalJvmCompilerRunner.kt:102)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.compileIncrementally(IncrementalCompilerRunner.kt:240)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.access$compileIncrementally(IncrementalCompilerRunner.kt:39)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner$compile$2.invoke(IncrementalCompilerRunner.kt:81)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.compile(IncrementalCompilerRunner.kt:93)
	at org.jetbrains.kotlin.daemon.CompileServiceImplBase.execIncrementalCompiler(CompileServiceImpl.kt:601)
	at org.jetbrains.kotlin.daemon.CompileServiceImplBase.access$execIncrementalCompiler(CompileServiceImpl.kt:93)
	at org.jetbrains.kotlin.daemon.CompileServiceImpl.compile(CompileServiceImpl.kt:1633)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at java.rmi/sun.rmi.server.UnicastServerRef.dispatch(UnicastServerRef.java:359)
	at java.rmi/sun.rmi.transport.Transport$1.run(Transport.java:200)
	at java.rmi/sun.rmi.transport.Transport$1.run(Transport.java:197)
	at java.base/java.security.AccessController.doPrivileged(Native Method)
	at java.rmi/sun.rmi.transport.Transport.serviceCall(Transport.java:196)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport.handleMessages(TCPTransport.java:562)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run0(TCPTransport.java:796)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.lambda$run$0(TCPTransport.java:677)
	at java.base/java.security.AccessController.doPrivileged(Native Method)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run(TCPTransport.java:676)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)
```

</td>
</tr>
<tr>
<td>

```groovy
android {
    // ...

    buildFeatures {
        compose true
    }
    // composeOptions {
    //     kotlinCompilerExtensionVersion compose_version
    //     kotlinCompilerVersion '1.4.10'
    // }
}
```

</td>
<td>

```
> Task :app:compileDebugKotlin FAILED
w: ATTENTION!
This build uses unsafe internal compiler arguments:

-XXLanguage:+NonParenthesizedAnnotationsOnFunctionalTypes

This mode is not recommended for production use,
as no stability/compatibility guarantees are given on
compiler or generated code. Use it at your own risk!

e: /Users/omar/git/ComposeOnStableAgp/app/src/main/java/com/github/nytimes/composeonstableagp/MainActivity.kt: (20, 54): 'background: Color' is only available since Kotlin 1.4 and cannot be used in Kotlin 1.3

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:compileDebugKotlin'.
> Compilation error. See log for more details

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org
```

after remove `color = MaterialTheme.colors.background`

```
> Task :app:compileDebugKotlin FAILED
w: ATTENTION!
This build uses unsafe internal compiler arguments:

-XXLanguage:+NonParenthesizedAnnotationsOnFunctionalTypes

This mode is not recommended for production use,
as no stability/compatibility guarantees are given on
compiler or generated code. Use it at your own risk!

e: java.lang.IllegalStateException: Cannot find the Composer class
	at androidx.compose.plugins.kotlin.compiler.lower.AbstractComposeLowering.<init>(AbstractComposeLowering.kt:144)
	at androidx.compose.plugins.kotlin.compiler.lower.ComposerLambdaMemoization.<init>(ComposerLambdaMemoization.kt:147)
	at androidx.compose.plugins.kotlin.ComposeIrGenerationExtension.generate(ComposeIrGenerationExtension.kt:95)
	at androidx.compose.plugins.kotlin.ComposeIrGenerationExtension.generate(ComposeIrGenerationExtension.kt:53)
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade.doGenerateFilesInternal$backend_jvm(JvmBackendFacade.kt:86)
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade.doGenerateFilesInternal$backend_jvm$default(JvmBackendFacade.kt:64)
	at org.jetbrains.kotlin.backend.jvm.JvmBackendFacade.doGenerateFilesInternal$backend_jvm(JvmBackendFacade.kt:52)
	at org.jetbrains.kotlin.backend.jvm.JvmIrCodegenFactory.generateModule(JvmIrCodegenFactory.kt:36)
	at org.jetbrains.kotlin.codegen.KotlinCodegenFacade.doGenerateFiles(KotlinCodegenFacade.java:47)
	at org.jetbrains.kotlin.codegen.KotlinCodegenFacade.compileCorrectFiles(KotlinCodegenFacade.java:39)
	at org.jetbrains.kotlin.cli.jvm.compiler.KotlinToJVMBytecodeCompiler.generate(KotlinToJVMBytecodeCompiler.kt:638)
	at org.jetbrains.kotlin.cli.jvm.compiler.KotlinToJVMBytecodeCompiler.compileModules$cli(KotlinToJVMBytecodeCompiler.kt:198)
	at org.jetbrains.kotlin.cli.jvm.K2JVMCompiler.doExecute(K2JVMCompiler.kt:172)
	at org.jetbrains.kotlin.cli.jvm.K2JVMCompiler.doExecute(K2JVMCompiler.kt:56)
	at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.kt:85)
	at org.jetbrains.kotlin.cli.common.CLICompiler.execImpl(CLICompiler.kt:43)
	at org.jetbrains.kotlin.cli.common.CLITool.exec(CLITool.kt:104)
	at org.jetbrains.kotlin.incremental.IncrementalJvmCompilerRunner.runCompiler(IncrementalJvmCompilerRunner.kt:349)
	at org.jetbrains.kotlin.incremental.IncrementalJvmCompilerRunner.runCompiler(IncrementalJvmCompilerRunner.kt:105)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.compileIncrementally(IncrementalCompilerRunner.kt:237)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.access$compileIncrementally(IncrementalCompilerRunner.kt:37)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner$compile$2.invoke(IncrementalCompilerRunner.kt:79)
	at org.jetbrains.kotlin.incremental.IncrementalCompilerRunner.compile(IncrementalCompilerRunner.kt:91)
	at org.jetbrains.kotlin.daemon.CompileServiceImplBase.execIncrementalCompiler(CompileServiceImpl.kt:606)
	at org.jetbrains.kotlin.daemon.CompileServiceImplBase.access$execIncrementalCompiler(CompileServiceImpl.kt:99)
	at org.jetbrains.kotlin.daemon.CompileServiceImpl.compile(CompileServiceImpl.kt:1645)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at java.rmi/sun.rmi.server.UnicastServerRef.dispatch(UnicastServerRef.java:359)
	at java.rmi/sun.rmi.transport.Transport$1.run(Transport.java:200)
	at java.rmi/sun.rmi.transport.Transport$1.run(Transport.java:197)
	at java.base/java.security.AccessController.doPrivileged(Native Method)
	at java.rmi/sun.rmi.transport.Transport.serviceCall(Transport.java:196)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport.handleMessages(TCPTransport.java:562)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run0(TCPTransport.java:796)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.lambda$run$0(TCPTransport.java:677)
	at java.base/java.security.AccessController.doPrivileged(Native Method)
	at java.rmi/sun.rmi.transport.tcp.TCPTransport$ConnectionHandler.run(TCPTransport.java:676)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)
```

</td>
</tr>
<tr>
<td>

```groovy
android {
    // ...

    // buildFeatures {
    //     compose true
    // }
    // composeOptions {
    //     kotlinCompilerExtensionVersion compose_version
    //     kotlinCompilerVersion '1.4.10'
    // }
}
```

</td>
<td>

```
BUILD SUCCESSFUL!
```

</td>
</tr>
<tr>
<td>

```groovy
android {
    // ...

    buildFeatures {
        compose true
    }
    composeOptions {
        kotlinCompilerExtensionVersion compose_version
        kotlinCompilerVersion '1.4.10'
    }
}
```

</td>
<td>

```

```

</td>
</tr>
</table>