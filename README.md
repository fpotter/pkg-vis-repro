# Minimal repro of issue with npm_translate_lock's package_visibility feature

Minimal repo for rules_js issue filed here: https://github.com/aspect-build/rules_js/issues/2345

### How to reproduce

Setup:

```sh
git clone git@github.com:fpotter/pkg-vis-repro.git
cd pkg-vis-repro
direnv allow
bazel run //tools:bazel_env
```

When package is imported as `//:node_modules/some-dep`, visibility is honored.  The following build will fail.

```sh
$ bazel build //packages/from-root
ERROR: /home/fpotter/git/pkg-vis-repro/packages/from-root/BUILD:13:11: in ts_project rule //packages/from-root:from-root: Visibility error:
target '//:node_modules/some-dep' is not visible from
target '//packages/from-root:from-root'
Recommendation: modify the visibility declaration if you think the dependency is legitimate. For more info see https://bazel.build/concepts/visibility
...
ERROR: Build did NOT complete successfully
```

When package is imported as `:node_modules/some-dep`, visibility not honored, but I'd expect it to be given `package_visibility` configuration in `npm_translate_lock` ([link](https://github.com/fpotter/pkg-vis-repro/blob/eb6abff09d5d888dc9f59f90287cdd8ac5b2639a/MODULE.bazel#L30)).  The following build succeeds.

```sh
$ bazel build //packages/from-local
...
INFO: Build completed successfully, 1 total action
```
