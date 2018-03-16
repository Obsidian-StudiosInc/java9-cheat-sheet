# Java 9 Cheat Sheet

Just a cheat sheet of fixes for Java 9 issues.
Contributions welcomed!

## --release
None of the following works with the --release < 9. Using --release 
6, 7, or 8; classes requiring exposure are not found at all. 
Forcing use of Java 9 and dropping --release to expose; com.sun.*, 
sun.*, etc. Though with --release 6, 7, or 8 things like 
javax.activation are auto loaded, without needing --add-modules. Pros 
and cons, when there is a choice.

You can use --release 9+ along with --add-modules or --add-exports.
Which really does not make sense till Java 10+.

## javax.activation
```
--add-modules java.activation
```
This will be removed from JDK11+. Need to use 
[JAF/javax-activation](https://github.com/javaee/activation)

## javax.annotation.Generated
```
--add-modules java.xml.ws.annotation
```

## javax.jnlp
```
--add-modules java.jnlp
```

## javax.xml
```
--add-modules java.xml
```

## javax.xml.bind
```
--add-modules java.xml.bind
```
This will be removed from JDK11+. Need to use 
[JSR-222 jaxb-api](https://github.com/javaee/jaxb-spec)

## com.sun.org.apache.xpath.internal
```
--add-exports=java.xml/com.sun.org.apache.xpath.internal.objects=ALL-UNNAMED
```

## sun.font
```
--add-exports java.desktop/sun.font=ALL-UNNAMED
```

## sun.misc.Unsafe
```
--add-exports jdk.unsupported/sun.misc=ALL-UNNAMED
```

## sun.security.x509
```
--add-exports=java.base/sun.security.x509=ALL-UNNAMED
```

## @Contended
```
sed -i -e "s|sun.misc.C|jdk.internal.vm.annotation.C|g" Class.java

--add-exports java.base/jdk.internal.vm.annotation=ALL-UNNAMED
```

## tools.jar
This has a bunch of stuff in it.

### com.sun.tools.javac
In simplest form, most things are not exposed.
```
--add-modules jdk.compiler
```

To expose various parts. Expose as needed, likely do not need all just examples.
```
--add-exports=jdk.compiler/com.sun.tools.javac=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.code=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.comp=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.main=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.model=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.parser=ALL-UNNAMED 
--add-exports=jdk.compiler/com.sun.tools.javac.processing=ALL-UNNAMED
--add-exports=jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED
```

### com.sun.tools.javadoc
```
--add-modules jdk.javadoc
```

## Cannot find resource
In some cases resources in the same folders as classes cannot be found 
during compile by some annotation processors. In those cases this can be 
a resolution.
```
--source-path src/main/java
```

## Notes
When things are not visible, you use the --add-exports to expose.

### Using --add-modules with --add-exports
Seems it is not necessary and redundant to add both. There is no harm. 
Seems --add-exports will add the module of the classes being exposed.
