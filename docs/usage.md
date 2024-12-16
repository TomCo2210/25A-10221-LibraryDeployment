# 6. Add Usage Instructions to the `README.md`

1. Include JitPack dependency details:
    - Add a `How to Use` section with instructions for adding the library as a dependency:

    ```markdown
    ## How to Use

    Add JitPack to your project-level `build.gradle` or `settings.gradle`:
        ```kotlin
        repositories {
            maven { url 'https://jitpack.io' }
        }
        ```
    ```

2. Add the library dependency to your app-level build.gradle:

    ```kotlin 
    dependencies {
        implementation ("com.github.your-username:your-library-name:1.0.0")
    }
    ```

    convert dependency to kotlin syntax using ```gradle/libs.versions.toml``` file

[Return to the README.md](../README.md)
