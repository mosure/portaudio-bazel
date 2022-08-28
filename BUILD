load('@rules_cc//cc:defs.bzl', 'cc_library')


cc_library(
    name = "portaudio-common",
    srcs = glob([
        "src/common/*.c",
    ]),
    hdrs = glob([
        "include/portaudio.h",
        "src/common/*.h",
    ]),
    includes = [
        "include",
        "src/common",
    ],
    visibility = ["//visibility:public"],
)


cc_library(
    name = "portaudio-wasapi",
    srcs = glob([
        "src/hostapi/wasapi/*.c",
    ]),
    hdrs = glob([
        "include/pa_win_wasapi.h",
        "src/hostapi/wasapi/mingw-include/*.h",
    ]),
    includes = [
        "src/hostapi/wasapi/mingw-include",
    ],
    defines = [
        "PA_USE_WASAPI=1",
    ],
    deps = [
        ":portaudio-common",
    ],
    linkopts = [
        '-DEFAULTLIB:ole32.lib',
        '-DEFAULTLIB:winmm.lib',
    ],
    visibility = ["//visibility:public"],
)


cc_library(
    name = "portaudio-windows",
    srcs = glob([
        "src/os/win/*.c",
    ]),
    hdrs = glob([
        "src/os/win/*.h",
    ]),
    includes = [
        "src/os/win",
    ],
    deps = [
        ":portaudio-common",
    ],
    visibility = ["//visibility:public"],
)


cc_library(
    name = "portaudio-directsound",
    srcs = glob([
        "src/hostapi/dsound/*.c",
    ]),
    hdrs = glob([
        "include/pa_win_ds.h",
        "src/hostapi/dsound/*.h",
    ]),
    includes = [
        "src/hostapi/dsound",
    ],
    defines = [
        "PA_USE_DS=1",
        "PAWIN_USE_DIRECTSOUNDFULLDUPLEXCREATE=1",
    ],
    deps = [
        ":portaudio-common",
        ":portaudio-windows",
    ],
    linkopts = [
        '-DEFAULTLIB:dsound3d.lib',
    ],
    visibility = ["//visibility:public"],
)


cc_library(
    name = "portaudio",
    deps = [ # TODO: add select based on platform
        ":portaudio-directsound",
    ],
    visibility = ["//visibility:public"],
)
