licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//visibility:public"])

load(
    "//third_party/tf:tensorflow_io.bzl",
    "tf_io_copts",
)

cc_library(
    name = "azfs_ops",
    srcs = [
        "azfs/azfs.cc",
        "azfs/azfs.h",
        "azfs/azfs_ops.cc",
    ],
    copts = tf_io_copts(),
    linkstatic = True,
    deps = [
        ":azfs_random_access_file",
        ":azfs_readonly_memory_region",
        ":azfs_writable_file",
    ],
)

cc_library(
    name = "azfs_client",
    srcs = [
        "azfs/azfs_client.cc",
    ],
    hdrs = [
        "azfs/azfs_client.h",
    ],
    copts = tf_io_copts(),
    linkstatic = True,
    deps = [
        "@com_github_azure_azure_storage_cpplite//:azure",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "azfs_writable_file",
    srcs = [
        "azfs/azfs_writable_file.cc",
    ],
    hdrs = [
        "azfs/azfs_writable_file.h",
    ],
    copts = tf_io_copts(),
    linkstatic = True,
    deps = [
        ":azfs_client",
    ],
)

cc_library(
    name = "azfs_random_access_file",
    srcs = [
        "azfs/azfs_random_access_file.cc",
    ],
    hdrs = [
        "azfs/azfs_random_access_file.h",
    ],
    copts = tf_io_copts(),
    linkstatic = True,
    deps = [
        ":azfs_client",
    ],
)

cc_library(
    name = "azfs_readonly_memory_region",
    srcs = [
        "azfs/azfs_readonly_memory_region.h",
    ],
    copts = tf_io_copts(),
    linkstatic = True,
    deps = [
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

# bazel test \
#   --action_env=TF_AZURE_USE_DEV_STORAGE=1 \
#   //tensorflow_io/azure:azfs_cc_test
cc_test(
    name = "azfs_cc_test",
    srcs = ["azfs/azfs_test.cc"],
    deps = [
        ":azfs_ops",
        "@com_google_googletest//:gtest",
        "@com_google_googletest//:gtest_main",
    ],
)
