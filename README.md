# Reproducer: Renovate & Version Catalog versions section

A Reproducer Project for 

* https://github.com/renovatebot/renovate/issues/12956 Renovate creates multiple PRs for common versions in gradle version catalog #12956

## Steps to get this project.

* Create a new AndroidX Compose Project from Android Studio.
* Enable Version Catalog `enableFeaturePreview("VERSION_CATALOGS")` in settings.gradle
* Add Version Catalog gradle/libs.versions.toml
* Declare `compose` version, and use it.

---

Gradle Version Catalog is:

```toml
[versions]
compose = "1.0.1"

[libraries]
compose-material = { module = "androidx.compose.material:material", version.ref = "compose" }
compose-ui = { module = "androidx.compose.ui:ui", version.ref = "compose" }
compose-ui-tooling = { module = "androidx.compose.ui:ui-tooling-preview", version.ref = "compose" }
```

## Current Behavior:

* Renovate makes 2 PRs for `androidx.compose.ui` and `androidx.compose.material` groups.
    * `androidx.compose.ui` -> https://github.com/irgaly/reproducer-renovate-12956-version-catalog/pull/2
    * `andoridx.compose.material` -> https://github.com/irgaly/reproducer-renovate-12956-version-catalog/pull/5
* They have same changes `compose = "1.1.0" in gradle/libs.versions.toml

## Expected Behavior:

* Renovate makes 1 PR for `androidx.compose.ui` and `androidx.compose.material` because `compose` version is in `[version]` section in Gradle Version Catalog and have same changes.
