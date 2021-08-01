# arch/arm64/boot/dts/vendor/qcom/lahaina.dtsi
```
/ {
:
    reserved_memory: reserved-memory { };
:
}

&reserved_memory {
:

	xbl_apps_hob_mem: xbl_apps_hob_mem@e3400000 {
		no-map;
		reg = <0x0 0xe3400000 0x0 0x1000>;
	};

:
}

```

# arch/arm64/boot/dts/oemc1/surface-duo-surface.dtsi
```
&soc {
:
    oem_smem: oem_smem@0xE3400000 {
	    compatible = "surface,oem-smem";
	    reg = <0xE3400000 0x1000>;
	};
};

```

# drivers/firmware/surface/xbl_hlos_hob.c
- int xbl_hlos_hob_init()
```
    np = of_find_compatible_node(NULL, NULL, "surface,oem-smem");
    if (!np)
    {
        pr_err("%s: can't find surface,oem-smem node\n", __func__);
        rc = -ENODEV;
        goto xbl_hlos_hob_init_exit;
    }

    XblHlosHob = of_iomap(np, 0);
```