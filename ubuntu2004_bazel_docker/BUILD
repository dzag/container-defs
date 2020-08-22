load(
    "@io_bazel_rules_docker//docker/toolchain_container:toolchain_container.bzl",
    "toolchain_container",
)

load("@io_bazel_rules_docker//container:container.bzl", "container_push")

package(default_visibility = ["//visibility:public"])

toolchain_container(
    name = "image",
    base = "@ubuntu2004//image",
    cmd = [
        "/bin/sh",
        "-c",
        "/bin/bash",
    ],
    env = {
        "LANG": "C.UTF-8",
        "LANGUAGE": "C.UTF-8",
        "LC_ALL": "C.UTF-8",
    },
    installation_cleanup_commands = "rm -f /etc/init.d/.depend.boot /etc/init.d/.depend.start /etc/init.d/.depend.stop",
    language_layers = [
        "@layer_defs//layers/ubuntu2004/clang:clang-ltl",
        "@layer_defs//layers/ubuntu2004/java:java-ltl",
        "@layer_defs//layers/ubuntu2004/python:python-ltl",
        "@layer_defs//layers/ubuntu2004/bazel:bazel-ltl",
        "@layer_defs//layers/ubuntu2004/docker:docker-ltl",
    ],
    stamp = True
)

container_push(
    name = "push_image",
    image = ":image",
    format = "Docker",
    registry = "index.docker.io",
    repository = "dzag/bazel-docker",
)