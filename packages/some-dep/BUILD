load("@aspect_rules_js//npm:defs.bzl", "npm_package")
load("@aspect_rules_ts//ts:defs.bzl", "ts_config", "ts_project")
load("@npm//:defs.bzl", "npm_link_all_packages")

npm_link_all_packages(name = "node_modules")

npm_package(
    name = "pkg",
    srcs = [
        "package.json",
        ":some-dep",
    ],
    visibility = ["//visibility:public"],
)

ts_project(
    name = "some-dep",
    srcs = ["src/index.ts"],
    composite = True,
    declaration = True,
    declaration_map = True,
    out_dir = "dist",
    preserve_jsx = False,
    resolve_json_module = True,
    root_dir = "src",
    source_map = True,
    tsconfig = ":tsconfig",
)

ts_config(
    name = "tsconfig",
    src = "tsconfig.json",
    deps = ["//:tsconfig_base"],
)
