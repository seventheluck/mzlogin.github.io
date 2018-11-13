---
layout: post
title: Java ClassLoader
categories: Java
description: Java ClassLoader
keywords: Java, ClassLoader
---
#### Overview
For learning java ClassLoader, we can start from three lines java code:
```java
public class LearningClassLoader {
    public static void main(String[] args) {
        System.out.println(LearningClassLoader.class.getClassLoader());
        System.out.println(Logging.class.getClassLoader());
        System.out.println(ClassLoader.class.getClassLoader());
    }
}
```
Above code will output these:

>sun.misc.Launcher$AppClassLoader@15db9742
>sun.misc.Launcher$ExtClassLoader@5c647e05
>null

These three outputs corresponding to three types of ClassLoader.

>First is the AppClassLoader.
>Second is the ExtClassLoader.
>Third is the Bootstrap ClassLoader.

Bootstrap ClassLoader is responsible for loading files in path "jre/lib".
ExtClassLoader is responsible for loading files in path "jre/lib/ext".
AppClassLoader is responsible for loading files in class path.

#### Lifecycle of the class

Loading --> Linking --> Initialization --> Using --> Unloading

Linking : Verification --> Preparation --> Resolution

```java

    static class ExtClassLoader extends URLClassLoader {
        public static Launcher.ExtClassLoader getExtClassLoader() throws IOException {
            final File[] var0 = getExtDirs();

            try {
                return (Launcher.ExtClassLoader)AccessController.doPrivileged(new PrivilegedExceptionAction<Launcher.ExtClassLoader>() {
                    public Launcher.ExtClassLoader run() throws IOException {
                        int var1 = var0.length;

                        for(int var2 = 0; var2 < var1; ++var2) {
                            MetaIndex.registerDirectory(var0[var2]);
                        }

                        return new Launcher.ExtClassLoader(var0);
                    }
                });
            } catch (PrivilegedActionException var2) {
                throw (IOException)var2.getException();
            }
        }

        void addExtURL(URL var1) {
            super.addURL(var1);
        }

        public ExtClassLoader(File[] var1) throws IOException {
            super(getExtURLs(var1), (ClassLoader)null, Launcher.factory);
            SharedSecrets.getJavaNetAccess().getURLClassPath(this).initLookupCache(this);
        }

        private static File[] getExtDirs() {
            String var0 = System.getProperty("java.ext.dirs");
            File[] var1;
            if (var0 != null) {
                StringTokenizer var2 = new StringTokenizer(var0, File.pathSeparator);
                int var3 = var2.countTokens();
                var1 = new File[var3];

                for(int var4 = 0; var4 < var3; ++var4) {
                    var1[var4] = new File(var2.nextToken());
                }
            } else {
                var1 = new File[0];
            }

            return var1;
        }

        private static URL[] getExtURLs(File[] var0) throws IOException {
            Vector var1 = new Vector();

            for(int var2 = 0; var2 < var0.length; ++var2) {
                String[] var3 = var0[var2].list();
                if (var3 != null) {
                    for(int var4 = 0; var4 < var3.length; ++var4) {
                        if (!var3[var4].equals("meta-index")) {
                            File var5 = new File(var0[var2], var3[var4]);
                            var1.add(Launcher.getFileURL(var5));
                        }
                    }
                }
            }

            URL[] var6 = new URL[var1.size()];
            var1.copyInto(var6);
            return var6;
        }

        public String findLibrary(String var1) {
            var1 = System.mapLibraryName(var1);
            URL[] var2 = super.getURLs();
            File var3 = null;

            for(int var4 = 0; var4 < var2.length; ++var4) {
                URI var5;
                try {
                    var5 = var2[var4].toURI();
                } catch (URISyntaxException var9) {
                    continue;
                }

                File var6 = Paths.get(var5).toFile().getParentFile();
                if (var6 != null && !var6.equals(var3)) {
                    String var7 = VM.getSavedProperty("os.arch");
                    File var8;
                    if (var7 != null) {
                        var8 = new File(new File(var6, var7), var1);
                        if (var8.exists()) {
                            return var8.getAbsolutePath();
                        }
                    }

                    var8 = new File(var6, var1);
                    if (var8.exists()) {
                        return var8.getAbsolutePath();
                    }
                }

                var3 = var6;
            }

            return null;
        }

        private static AccessControlContext getContext(File[] var0) throws IOException {
            PathPermissions var1 = new PathPermissions(var0);
            ProtectionDomain var2 = new ProtectionDomain(new CodeSource(var1.getCodeBase(), (Certificate[])null), var1);
            AccessControlContext var3 = new AccessControlContext(new ProtectionDomain[]{var2});
            return var3;
        }

        static {
            ClassLoader.registerAsParallelCapable();
        }
    }

```