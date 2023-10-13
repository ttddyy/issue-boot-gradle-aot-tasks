# About

Simple gradle multi module project.

- Using old style - `buildscript`, `[all|sub]projects` to specify spring-boot plugin

# Issue

`nativeCompile` does not include AOT related tasks.

**Expected:**
```
> ./gradlew -m nativeCompile
:server:compileJava SKIPPED
:server:processResources SKIPPED
:server:classes SKIPPED
:server:resolveMainClassName SKIPPED    // expected
:server:processAot SKIPPED              // expected
:server:compileAotJava SKIPPED          // expected
:server:processAotResources SKIPPED     // expected
:server:aotClasses SKIPPED              // expected
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

`build` task

```
> ./gradlew -m build
:compileJava SKIPPED
:processResources SKIPPED
:classes SKIPPED
:jar SKIPPED
:assemble SKIPPED
:compileTestJava SKIPPED
:processTestResources SKIPPED
:testClasses SKIPPED
:test SKIPPED
:check SKIPPED
:build SKIPPED
:server:compileJava SKIPPED
:server:processResources SKIPPED
:server:classes SKIPPED
:server:resolveMainClassName SKIPPED
:server:processAot SKIPPED
:server:compileAotJava SKIPPED
:server:processAotResources SKIPPED
:server:aotClasses SKIPPED
:server:bootJar SKIPPED
:server:jar SKIPPED
:server:assemble SKIPPED
:server:compileTestJava SKIPPED
:server:processTestResources SKIPPED
:server:testClasses SKIPPED
:server:processTestAot SKIPPED
:server:compileAotTestJava SKIPPED
:server:processAotTestResources SKIPPED
:server:aotTestClasses SKIPPED
:server:test SKIPPED
:server:check SKIPPED
:server:build SKIPPED
```

# Fix and Root Cause

ClassLoader that loads Boot's Gradle plugin can't see the NBT plugin's types as they're only visible to the subproject's ClassLoader.

See the change: https://github.com/ttddyy/issue-boot-gradle-aot-tasks/commit/ed85440a01bba5f74249f8f2bfefe8e72491b545

