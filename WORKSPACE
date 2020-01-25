# Android SDK.
android_sdk_repository(name = "androidsdk")

# TODO(BenHenning): Maybe convert all of these HTTP archives to Git repositories, and later to the Bazel Federation when it's no longer experimental.

# Add support for installing third party Bazel rules from HTTP archives.
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Add support for loading third party libraries from Maven. For context, see:
# https://github.com/bazelbuild/rules_jvm_external
RULES_JVM_EXTERNAL_TAG = "3.0"
RULES_JVM_EXTERNAL_SHA = "62133c125bf4109dfd9d2af64830208356ce4ef8b165a6ef15bbff7460b35c3a"
http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)
load("@rules_jvm_external//:defs.bzl", "maven_install")

# Add support for protobuf: https://github.com/bazelbuild/rules_proto.
http_archive(
    name = "rules_proto",
    sha256 = "602e7161d9195e50246177e7c55b2f39950a9cf7366f74ed5f22fd45750cd208",
    strip_prefix = "rules_proto-97d8af4dc474595af3900dd85cb3a29ad28cc313",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
    ],
)
load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()

# Add support for Javalite protobuf.
http_archive(
    name = "com_google_protobuf_javalite",
    urls = ["https://github.com/google/protobuf/archive/javalite.zip"],
    strip_prefix = "protobuf-javalite",
)

# Add support for Python: https://github.com/bazelbuild/rules_python.
http_archive(
    name = "rules_python",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.0.1/rules_python-0.0.1.tar.gz",
    sha256 = "aa96a691d3a8177f3215b14b0edc9641787abaaa30363a080165d06ab65e1161",
)

# Add support for Kotlin: https://github.com/bazelbuild/rules_kotlin.
RULES_KOTLIN_VERSION = "legacy-1.3.0-rc4"
RULES_KOTLIN_SHA = "fe32ced5273bcc2f9e41cea65a28a9184a77f3bc30fea8a5c47b3d3bfc801dff"
http_archive(
    name = "io_bazel_rules_kotlin",
    urls = ["https://github.com/bazelbuild/rules_kotlin/archive/%s.zip" % RULES_KOTLIN_VERSION],
    type = "zip",
    strip_prefix = "rules_kotlin-%s" % RULES_KOTLIN_VERSION,
    sha256 = RULES_KOTLIN_SHA,
)
load("@io_bazel_rules_kotlin//kotlin:kotlin.bzl", "kotlin_repositories", "kt_register_toolchains")
kotlin_repositories()
kt_register_toolchains()

# Download all third party libraries needed for Oppia Android.
KOTLIN_LIB_VERSION = "1.3.41"
maven_install(
    artifacts = [
        "androidx.appcompat:appcompat:1.0.2",
        "androidx.lifecycle:lifecycle-livedata-ktx:2.2.0-alpha03",
        "com.github.bumptech.glide:glide:4.9.0",
        "com.google.dagger:dagger:2.24",
        "org.jetbrains.kotlin:kotlin-stdlib-jdk7:%s" % KOTLIN_LIB_VERSION,
    ],
    repositories = [
        "https://jcenter.bintray.com/",
        "https://dl.google.com/dl/android/maven2/",
        "https://repo.maven.apache.org/maven2/",
    ],
)
