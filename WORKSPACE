### Android rules
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_android",
    sha256 = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806",
    strip_prefix = "rules_android-0.1.1",
    urls = ["https://github.com/bazelbuild/rules_android/archive/v0.1.1.zip"],
)

load("@rules_android//android:rules.bzl", "android_sdk_repository")

android_sdk_repository(
    name = "androidsdk",
    build_tools_version = "33.0.0",
)

# Setup Maven so the project can download external dependencies
RULES_JVM_EXTERNAL_TAG = "5.2"

RULES_JVM_EXTERNAL_SHA = "c9ae901381ae7f7eca08aed96caeb542f96c5449052db9c9d27274a8dc154cdf"

http_archive(
    name = "rules_jvm_external",
    sha256 = RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.tar.gz" % RULES_JVM_EXTERNAL_TAG,
)
load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("@rules_jvm_external//:defs.bzl", "maven_install")

# Setup Kotlin rules
rules_kotlin_version = "1.7.1"

rules_kotlin_sha = "fd92a98bd8a8f0e1cdcb490b93f5acef1f1727ed992571232d33de42395ca9b3"

http_archive(
    name = "io_bazel_rules_kotlin",
    sha256 = rules_kotlin_sha,
    urls = ["https://github.com/bazelbuild/rules_kotlin/releases/download/v%s/rules_kotlin_release.tgz" % rules_kotlin_version],
)

load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories")

kotlin_repositories()

load("@io_bazel_rules_kotlin//kotlin:core.bzl", "kt_register_toolchains")

kt_register_toolchains()  # to use the default toolchain, otherwise see toolchains below

maven_install(
    artifacts = [
        "androidx.constraintlayout:constraintlayout:2.2.0-alpha07",
        "androidx.constraintlayout:constraintlayout-core:1.0.4",
    ],
    # If 'maven_install_json' is enabled, rendering in AS does not work
    # maven_install_json = "@//:maven_install.json",
    fetch_sources = True,
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
    strict_visibility = True,
    version_conflict_policy = "pinned",
)

load("@maven//:defs.bzl", "pinned_maven_install")
pinned_maven_install()
