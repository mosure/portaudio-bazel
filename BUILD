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
    name = "portaudio-wasapi",
    srcs = glob([
        "src/hostapi/wasapi/pa_win_wasapi.c",
    ]),
    hdrs = glob([
        "include/pa_win_wasapi.h",
    ]),
    includes = [
    ],
    defines = [
        "PA_USE_WASAPI=1",
    ],
    deps = [
        ":portaudio-common",
        ":portaudio-windows",
    ],
    linkopts = [
        '-DEFAULTLIB:kernel32.lib',
        '-DEFAULTLIB:user32.lib',
        '-DEFAULTLIB:gdi32.lib',
        '-DEFAULTLIB:winspool.lib',
        '-DEFAULTLIB:comdlg32.lib',
        '-DEFAULTLIB:advapi32.lib',
        '-DEFAULTLIB:shell32.lib',
        '-DEFAULTLIB:ole32.lib',
        '-DEFAULTLIB:oleaut32.lib',
        '-DEFAULTLIB:uuid.lib',
        '-DEFAULTLIB:odbc32.lib',
        '-DEFAULTLIB:odbccp32.lib',
        '-DEFAULTLIB:winmm.lib',
        '-DEFAULTLIB:setupapi.lib',
        '-DEFAULTLIB:ksuser.lib',
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
    deps = [
        ":portaudio-wasapi",
    ],
    visibility = ["//visibility:public"],
)
