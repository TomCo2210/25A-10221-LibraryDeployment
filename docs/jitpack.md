# 3. Configure the Library for JitPack

1. Update the `libs.versions.toml` file:

    - Include Maven Publication plugin by adding to the `libs.versions.toml` file:

    ```toml
    [plugins]
    maven-publish = { id = "maven-publish" }
    ```

2. Update the `build.gradle` file (library module): Ensure you apply the maven-publish plugin:

    ```kotlin
    plugins {
        alias(libs.plugins.android.library)
        alias(libs.plugins.maven.publish) // Apply the maven-publish plugin
    }

    ...

    afterEvaluate {
        publishing {
            publications {
                create<MavenPublication>("release") {
                    groupId = 'com.github.your-username'
                    artifactId = 'your-library-name'
                    version = '1.0.0' // Change as needed
                    artifact(tasks.getByName("bundleReleaseAar"))
                }
            }
        }
    }
    ```

3. Define the library’s version and artifact details: Replace `groupId`, `artifactId`, and `version` with meaningful identifiers.

4. Configure JitPack settings by adding `jitpack.yaml` file at the root of your repository:

    ```yaml
    jdk:
      - openjdk17
    ```

    - This file specifies the JDK version to use for building your library.
    - JitPack supports various JDK versions, including OpenJDK 8, 11, 14, 17, and more.
    - Android projects using Android Gradle plugin 8.0 and above can use Minimum version 17 of OpenJDK.

[Return to the README.md](../README.md)
