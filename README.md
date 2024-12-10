# 25A-10221-LibraryDeployment

## 1. Prepare Your Project

Before deploying your library, ensure your project is structured and ready for publishing.

1. Set up your library project:

    - Create a new project or refactor an existing one into a library module.
    - Use Android Studio or IntelliJ IDEA to create a module: `File -> New -> New Module -> Android Library` (for Android) or a plain Java/Kotlin library module.
2. Organize your files:

    - Place reusable code inside the library module.
    - Include clear `README.md` documentation at the root of your repository.
    - Add a `LICENSE` file (e.g., MIT, Apache 2.0) to specify the library's usage terms.
    - Include a .gitignore file to exclude unnecessary files from version control.
    - Ensure your library code is well-documented and tested.
    - Add sample code or a demo app to showcase the library's features.
3. Add a `build.gradle` file:

    - Ensure your library module has a `build.gradle` file with proper dependencies and configurations.
    - Include configurations for publishing (details below).

## 2. Push Your Project to GitHub

1. Create a GitHub repository:

    - Go to [GitHub](https://github.com/), create a new repository, and give it a meaningful name.
    - Initialize it with a .gitignore file for Java/Kotlin/Android if necessary.
2. Push your project to the repository:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/your-username/your-repo-name.git
git push -u origin main
```

## 3. Configure the Library for JitPack

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

## 4. Tag Your Release on GitHub

1. Create a Git tag:

    - A Git tag is required for JitPack to identify the version to publish.

    ```bash
    git tag v1.0.0
    git push origin v1.0.0
    ```

2. Verify the tag on GitHub:
    - Go to your repository → `Tags` section to ensure the tag is visible.

## 5. Publish with JitPack

1. Go to JitPack:

    - Visit [JitPack](https://jitpack.io/)'s website.
2. Find your GitHub repository:

    - Enter your GitHub repository URL (e.g., `https://github.com/your-username/your-repo-name`).
3. Build the project:

    - Select the version (tag) you created and click on ```Get It```.
4. Test the build:
    - If the build is successful, you'll see the dependency details for adding the library to other projects.

## 6. Add Usage Instructions to the `README.md`

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

## 7. Test the Published Library

1. Create a new sample project:

    - Create a fresh project and add your library dependency.
    - Test the library to ensure it works as expected.
2. Iterate and improve:

    - Fix any issues and create new Git tags for updates.
    - Push the changes to GitHub and JitPack for new releases.

## 8. Maintain and Update

1. For new releases:

    - Make changes in your library code.
    - Increment the `version` in `build.gradle`.
    - Create a new Git tag and push it to GitHub.
2. Announce changes:

    - Update your `README.md` with release notes and usage examples.