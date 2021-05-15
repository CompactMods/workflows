# CM Workflows
A repository hosting examples for building Minecraft mods using ForgeGradle 4 and Gradle.

## Required Setup
These workflows assume several things about your gradle setup. Anything that has to do with builds require you to set up a properties file with specific fields, and the build gradle file to follow certain patterns.

Any workflow that requires a specific set of properties will have them listed here. Check the `vars` step in the action file for a definitive list.

## Changelogs (manual-changelog)
See the `manual-changelog` workflow for more information. This uses the two changelog files under `.github` in order to compile a commit changelog between two versions.

The action will find the latest tag in the format `v*` and the one before it, and compile the changelog based on all the commits between the two.

## CI Tests (ci-tests)
Provides automated build testing using the Gradle wrapper. This is set up to ignore the Minecraft-tagged unit tests.

### Required Properties
| Property | Value
| --- | ---
| mod_id | Standard mod ID
| mod_version | Your mod's semver version (ie 1.0.0)

## Manual Build (manual-build)
Provides automated build testing using the Gradle wrapper. This is set up to ignore the Minecraft-tagged unit tests.

### Required Properties
| Property | Value
| --- | ---
| mod_id | Standard mod ID
| mod_version | Your mod's semver version (ie 1.0.0)

## Github Packages (manual-gh-packages)
The Github and Tagged Release workflows upload final results to Github Packages via the publish task.

Note that packages requires a specific line added to your build.gradle file, so it can properly deploy to Maven. Your modid must be all lowercase (important) and you should have the following added to the artifact definition for the main package:

```gradle
 publications {
    maven(MavenPublication) {
        artifactId = mod_id // <<< this line here
        artifacts {
            artifact jar
        }
    }
    // [snip]
 }
```

[You can find this in the example build file.](https://github.com/CompactMods/workflows/blob/main/build.gradle#L231-L240)

### Required Properties
| Property | Value
| --- | ---
| mod_id | Standard mod ID
| mod_version | Your mod's semver version (ie 1.0.0)
## CurseForge
Another thing the full versioned publish workflow does is automatic release to GitHub Packages and Curseforge. 

### Requirements
- Gradle properties, as specified below.
- Set a secret on your repository (or org) called `CF_API_TOKEN`.
- Set up the requirements for the `CHANGELOG` section. A markdown-based changelog will automatically build between the two version tags.
- 
### Required Properties
| Property | Value
| --- | ---
| mod_id | Standard mod ID. Used in build file by default.
| mod_version | Your mod's semver version (ie 1.0.0)
| cf_project | Numeric CF project ID. Find it on your mod page sidebar.
| cf_release_type | alpha, beta, or release


