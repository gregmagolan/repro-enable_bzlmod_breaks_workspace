# Repro of Bazel issue [#17289](https://github.com/bazelbuild/bazel/issues/17289)

Shows how the `--enable_bzlmod` flag (even with an empty `MODULE.bazel` file) breaks toolchain resolution for toolchains registered in the WORKSPACE file.

```
bazel run //:bin
```

works while,

```
bazel run //:bin --enable_bzlmod
```

fails with

```
ERROR: /Users/greg/aspect/oss/repro-enable_bzlmod_breaks_workspace/BUILD.bazel:3:10: While resolving toolchains for target //:bin: No matching toolchains found for types @rules_nodejs//nodejs:toolchain_type.
To debug, rerun with --toolchain_resolution_debug='@rules_nodejs//nodejs:toolchain_type'
If platforms or toolchains are a new concept for you, we'd encourage reading https://bazel.build/concepts/platforms-intro.
ERROR: Analysis of target '//:bin' failed; build aborted: 
INFO: Elapsed time: 3.519s
INFO: 0 processes.
ERROR: Build failed. Not running target
FAILED: Build did NOT complete successfully (61 packages loaded, 257 targets configured)
```
