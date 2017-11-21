# Java 9 Cheat Sheet

Just a cheat sheet of fixes for Java 9 issues.
Contributions welcomed!

## javax.activation
```
--add-modules java.activation
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

## com.sun.org.apache.xpath.internal
```
--add-exports=java.xml/com.sun.org.apache.xpath.internal.objects=ALL-UNNAMED
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

## Notes
When things are not visible, you use the --add-exports to expose.
