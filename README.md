# Arend Tutorial

Source code & exercises for Arend's tutorial.

### Part I

See [index.ard](PartI/src/index.ard) and the [online tutorial][tut1].

[tut1]: https://arend-lang.github.io/documentation/tutorial/PartI

### Running

The tutorial code depends on `arend-lib`. Both `arend-lib` and the Arend CLI
are part of the [Arend repository](https://github.com/JetBrains/Arend); after
building it (`./gradlew :cli:jarDep`) you can typecheck the tutorial with:

```
java -jar <path-to-Arend>/cli/build/libs/cli-1.11.0-full.jar \
     -L <path-to-Arend> -L <path-to-tutorial-code> PartI
```

`-L` adds a library search root; the positional argument names the library
(`PartI` or `PartII`) by its directory name. Pass `-r` to force a full
recompile and ignore the `.arc` binary cache.
