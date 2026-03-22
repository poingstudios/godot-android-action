# godot-android-action

A GitHub Action to build Godot Android Plugins (standard or mono).

This action automatically downloads the appropriate Godot `.aar` library based on your specified Godot version, compiles your Android plugin using Gradle, moves your `.gdap` file into the output directory, and uploads the built artifact as a `.zip` file for easy downloading or use in subsequent workflow steps.

## Usage

Create a workflow file (e.g., `.github/workflows/build.yml`) in your repository:

```yaml
name: Build Android Plugin
on:
  push:
    branches:
      - main
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '11'

      - name: Build Godot Android Plugin
        uses: your-username/godot-android-action@v1 # Replace with the actual action path
        with:
          godot_version: '3.5.1'
          project_path: './plugin'
          godot-lib_folder_path: 'godot-lib'
          gdap_file_path: 'plugin/my_plugin.gdap'
```

## Inputs

| Name | Description | Default | Required |
| --- | --- | --- | --- |
| `godot_version` | The version of Godot to be built (e.g., 3.5, 3.5.1). | N/A | Yes |
| `build_version` | The build version of Godot (`stable`, `rc1`, `beta1`). Note: `alpha` or `pre-alpha` might not work. | `stable` | No |
| `project_path` | The path of the project. | N/A | Yes |
| `godot-lib_folder_path` | The path of the godot-lib folder. | `godot-lib` | Yes |
| `gdap_file_path` | The path of the `.gdap` file. | N/A | Yes |
| `gradlew_build_path` | The path to the `gradlew` build script. | `./` | No |
| `upload_artifact_retention_days` | Retention days to keep the artifact. | `90` | No |

## Outputs

| Name | Description |
| --- | --- |
| `artifact_name` | Artifact name of the exported `.zip` file. |
