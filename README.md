# JavaPoetic

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-JavaPoetic-green.svg?style=flat)](https://android-arsenal.com/details/1/2153)
[![Download](https://api.bintray.com/packages/yongjhih/maven/JavaPoetic/images/download.svg) ](https://bintray.com/yongjhih/maven/JavaPoetic/_latestVersion)
[![JitPack](https://img.shields.io/github/tag/yongjhih/JavaPoetic.svg?label=JitPack)](https://jitpack.io/#yongjhih/JavaPoetic)
[![Build Status](https://travis-ci.org/yongjhih/JavaPoetic.svg)](https://travis-ci.org/yongjhih/JavaPoetic)
[![Join the chat at https://gitter.im/yongjhih/JavaPoetic](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/yongjhih/JavaPoetic?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![art/java-poetic.png](art/java-poetic.png)

JavaPoet Simple Builder.

Square JavaPoet: https://github.com/square/javapoet

For JavaPoet example:

```java
package com.example.helloworld;

public final class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello, JavaPoet!");
  }
}
```

Before:

```java
MethodSpec main = MethodSpec.methodBuilder("main")
    .addModifiers(Modifier.PUBLIC, Modifier.STATIC)
    .returns(void.class)
    .addParameter(String[].class, "args")
    .addStatement("$T.out.println($S)", System.class, "Hello, JavaPoet!")
    .build();

TypeSpec helloWorld = TypeSpec.classBuilder("HelloWorld")
    .addModifiers(Modifier.PUBLIC, Modifier.FINAL)
    .addMethod(main)
    .build();

JavaFile javaFile = JavaFile.builder("com.example.helloworld", helloWorld)
    .build();

javaFile.emit(System.out);
```

After:

```java
JavaFile javaFile = PoeticFile.Of.packages("com.example.helloworld").of(
            PoeticClass.Of.publics().classes("HelloWorld").method(
                PoeticMethod.Of.publics().statics().voids().name("main").parameter(String.class, "args").statement(
                    PoeticStatement.of("$T.out.println($S)", System.class, "Hello, JavaPoet!")
                )
            )
        );

javaFile.emit(System.out);
```

## Installation

```gradle
repositories {
    maven { url "https://jitpack.io" }
}

dependencies {
    compile 'com.github.yongjhih:javapoetic:-SNAPSHOT'
}
```

via jcenter:

```gradle
repositories {
    jcenter()
}

dependencies {
    compile 'com.infstory:javapoetic:1.0.0'
}
```

## Test

```bash
./gradlew test
```

## License

```
Copyright 2015 8tory, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

