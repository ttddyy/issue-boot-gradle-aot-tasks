# About

Simple gradle multi module project.

- Using old style - `buildscript`, `[all|sub]projects`

# Issue

`nativeCompile` does not include AOT related tasks.

**Expected:**
```
> ./gradlew -m nativeCompile
:server:compileJava SKIPPED
:server:processResources SKIPPED
:server:classes SKIPPED
:server:resolveMainClassName SKIPPED
:server:processAot SKIPPED
:server:compileAotJava SKIPPED
:server:processAotResources SKIPPED
:server:aotClasses SKIPPED
:server:jar SKIPPED
:server:generateResourcesConfigFile SKIPPED
:server:nativeCompile SKIPPED
```

**Actual:**

```
> ./gradlew -m nativeCompile
:server:compileJava SKIPPED
:server:processResources SKIPPED
:server:classes SKIPPED
:server:jar SKIPPED
:server:generateResourcesConfigFile SKIPPED
:server:nativeCompile SKIPPED
```

