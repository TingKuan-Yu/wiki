# build/soong/README.md

# Soong Config Variables

When converting vendor modules that contain conditionals, simple conditionals
can be supported through Soong config variables using `soong_config_*`
modules that describe the module types, variables and possible values:

```
soong_config_module_type {
    name: "acme_cc_defaults",
    module_type: "cc_defaults",
    config_namespace: "acme",
    variables: ["board"],
    bool_variables: ["feature"],
    value_variables: ["width"],
    properties: ["cflags", "srcs"],
}

soong_config_string_variable {
    name: "board",
    values: ["soc_a", "soc_b"],
}
```

This example describes a new `acme_cc_defaults` module type that extends the
`cc_defaults` module type, with three additional conditionals based on
variables `board`, `feature` and `width`, which can affect properties `cflags`
and `srcs`.

The values of the variables can be set from a product's `BoardConfig.mk` file:
```
SOONG_CONFIG_NAMESPACES += acme
SOONG_CONFIG_acme += \
    board \
    feature \

SOONG_CONFIG_acme_board := soc_a
SOONG_CONFIG_acme_feature := true
SOONG_CONFIG_acme_width := 200
```

The `acme_cc_defaults` module type can be used anywhere after the definition in
the file where it is defined, or can be imported into another file with:
```
soong_config_module_type_import {
    from: "device/acme/Android.bp",
    module_types: ["acme_cc_defaults"],
}
```

It can used like any other module type:
```
acme_cc_defaults {
    name: "acme_defaults",
    cflags: ["-DGENERIC"],
    soong_config_variables: {
        board: {
            soc_a: {
                cflags: ["-DSOC_A"],
            },
            soc_b: {
                cflags: ["-DSOC_B"],
            },
        },
        feature: {
            cflags: ["-DFEATURE"],
        },
        width: {
            cflags: ["-DWIDTH=%s"],
        },
    },
}

cc_library {
    name: "libacme_foo",
    defaults: ["acme_defaults"],
    srcs: ["*.cpp"],
}
```

With the `BoardConfig.mk` snippet above, libacme_foo would build with
cflags "-DGENERIC -DSOC_A -DFEATURE -DWIDTH=200".

`soong_config_module_type` modules will work best when used to wrap defaults
modules (`cc_defaults`, `java_defaults`, etc.), which can then be referenced
by all of the vendor's other modules using the normal namespace and visibility
rules.