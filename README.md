# Scala Native Sample

## Configuration
You may need to configure *build.sbt* to set the path to `clang` and `clang++`.

```
nativeMode := "release"
nativeClang := file("/usr/local/Cellar/llvm/4.0.0/bin/clang")
nativeClangPP := file("/usr/local/Cellar/llvm/4.0.0/bin/clang++")
```

## Fibonacci number (50 th)
Run on MBP (2.5GHz Intel Core i5)

|              | Naive       | Tail call     | Mutual tail call |
|--------------|:------------|:--------------|:-----------------|
| Scala Native | 103.52 secs | 0.034 *msecs* | 38.88 secs       |
| JVM          | 75.58 secs  | 0.430 *msecs* | 69.88 secs       |

### Scala Native
```
$ sbt compile nativeLink
...

$ time target/scala-2.11/scala-native-example-out 50
Naive fibonacci: 12586269025
Time: 103517377024 ns
Tail call fibonacci: 12586269025
Time: 34048 ns
Mutual tail call fibonacci: 12586269025
Time: 38880023040 ns

real	2m22.424s
user	2m22.243s
sys	0m0.060s
```

### Scala on JVM
```
# disable "enablePlugins(ScalaNativePlugin)" in build.sbt

$ sbt assembly
...

$ time java -jar target/scala-2.11/scala-native-example-assembly-0.1.0.jar 50
Naive fibonacci: 12586269025
Time: 75578138895 ns
Tail call fibonacci: 12586269025
Time: 429532 ns
Mutual tail call fibonacci: 12586269025
Time: 69880392492 ns

real	2m25.778s
user	2m25.700s
sys	0m0.164s
```
