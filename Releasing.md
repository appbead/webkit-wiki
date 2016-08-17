This is a work in progress; see https://trac.webkit.org/wiki/WebKitGTK/Releasing for example of good document

### Make tarball

```
Tools/gtk/make-dist.py -t qtwebkit -p Qt --version tp3 -c Tools/qt/manifest.txt
```

* `-c` option unpacks generated `.tar` file and builds it
* You may need to set environment variables when running `make-dist.py`, if default build options are not suitable, e.g.
```
CMAKE_PREFIX_PATH=/opt/Qt5.4.0/5.4/gcc_64 CC=/usr/bin/clang CXX=/usr/lib/ccache/clang++ Tools/gtk/make-dist.py ...
```

### Patch
```diff
diff --git a/Tools/gtk/make-dist.py b/Tools/gtk/make-dist.py
index a989b8b..cf19431 100755
--- a/Tools/gtk/make-dist.py
+++ b/Tools/gtk/make-dist.py
@@ -192,6 +192,8 @@ class Manifest(object):
             self.add_rule(Rule(Rule.Result.EXCLUDE, parts[1]))
         elif parts[0] == "include" and len(parts) > 1:
             self.add_rule(Rule(Rule.Result.INCLUDE, parts[1]))
+        else:
+            raise Exception('Line does not begin with a correct rule:\n\t' + line)

     def should_skip_file(self, directory, filename):
         # Only allow files that are not in version control when they are explicitly included in the manifest from the build dir.
@@ -242,7 +244,7 @@ class Distcheck(object):
         create_dir(build_dir, "build")
         create_dir(install_dir, "install")

-        command = ['cmake', '-DPORT=GTK', '-DCMAKE_INSTALL_PREFIX=%s' % install_dir, '-DCMAKE_BUILD_TYPE=Release', dist_dir]
+        command = ['cmake', '-DPORT=Qt', '-DCMAKE_INSTALL_PREFIX=%s' % install_dir, '-DCMAKE_BUILD_TYPE=Release', dist_dir]
         subprocess.check_call(command, cwd=build_dir)

     def build(self, build_dir):
@@ -290,7 +292,7 @@ if __name__ == "__main__":


     def get_tarball_root_and_output_filename_from_arguments(arguments):
-        tarball_root = "webkitgtk"
+        tarball_root = "qtwebkit"
         if arguments.version is not None:
             tarball_root += '-' + arguments.version
```