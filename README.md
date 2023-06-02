# sample-constraintlayout-bazel-app
Setup Bazel app with basic ConstraintLayout for render testing in Android Studio Bazel Plugin

# Pinned Setup
- Change the WORKSPACE file to uncomment the line under `maven_install`

    `# maven_install_json = "@//:maven_install.json",` 
    
    to 
    
    `maven_install_json = "@//:maven_install.json",`

- Sync the project in Android Studio with the Bazel Plugin and then search for the file

`bazel-bin/external/maven/androidx_constraintlayout_constraintlayout-1367678569.intellij-info.txt`

Inside the file there is an attribute `is_source` and it is defined as `false`. This is different when using the unpinned setup and this prevents it from rendering with the plugin.

```json
android_aar_ide_info {
  aar {
    is_external: true
    is_new_external_version: true
    is_source: false
    relative_path: "external/maven/androidx/constraintlayout/constraintlayout/2.2.0-alpha07/constraintlayout-2.2.0-alpha07.aar"
    root_execution_path_fragment: "bazel-out/darwin-fastbuild/bin"
  }
}
...
```

# Unpinned Setup
- Change the WORKSPACE file to comment the line under `maven_install`

    `maven_install_json = "@//:maven_install.json",` 
    
    to 
    
    `# maven_install_json = "@//:maven_install.json",`

- Sync the project in Android Studio with the Bazel Plugin and then search for the file

`bazel-bin/external/maven/androidx_constraintlayout_constraintlayout-1367678569.intellij-info.txt`

Inside the file there is an attribute `is_source` and it is defined as `true`, when this is set to `true` the AS Plugin renders the constraintlayout properly. 

```json
android_aar_ide_info {
  aar {
    is_external: true
    is_new_external_version: true
    is_source: true
    relative_path: "v1/https/maven.google.com/androidx/constraintlayout/constraintlayout/2.2.0-alpha07/constraintlayout-2.2.0-alpha07.aar"
    root_execution_path_fragment: "external/maven"
  }
}
...
```