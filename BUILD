load("@aspect_rules_ts//ts:defs.bzl", "ts_config")

"""Targets in the repository root"""

# We prefer BUILD instead of BUILD.bazel
# gazelle:build_file_name BUILD

load("@gazelle//:def.bzl", "gazelle")
load("@npm//:defs.bzl", "npm_link_all_packages")

# TODO: remove once https://github.com/aspect-build/aspect-cli/issues/560 done
# gazelle:js_npm_package_target_name pkg
npm_link_all_packages(name = "node_modules")

gazelle(
    name = "gazelle",
    gazelle = "@multitool//tools/gazelle",
)

ts_config(
    name = "tsconfig_base",
    src = "tsconfig.base.json",
    visibility = ["//visibility:public"],
)
