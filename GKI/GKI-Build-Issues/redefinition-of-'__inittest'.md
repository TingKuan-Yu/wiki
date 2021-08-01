


b"/s/kernel/msm-5.4/drivers/firmware/qcom_scm.c:1256:1: error: redefinition of '__inittest'\n" b'early_initcall(scm_mem_protection_init);\n' b'^\n' b"/s/kernel/msm-5.4/include/linux/module.h:110:29: note: expanded from macro 'early_initcall'\n" b'#define early_initcall(fn)              module_init(fn)\n' b'                                        ^\n' b"/s/kernel/msm-5.4/include/linux/module.h:130:42: note: expanded from macro 'module_init'\n" b'        static inline initcall_t __maybe_unused __inittest(void)                \\\n' b'                                                ^\n' b'/s/kernel/msm-


5.4/drivers/firmware/qcom_scm.c:1248:1: note: previous definition is here\n' b'subsys_initcall(qcom_scm_init);\n' b'^\n' b"/s/kernel/msm-5.4/include/linux/module.h:116:30: note: expanded from macro 'subsys_initcall'\n" b'#define subsys_initcall(fn)             module_init(fn)\n' b'                                        ^\n' b"/s/kernel/msm-5.4/include/linux/module.h:130:42: note: expanded from macro 'module_init'\n" b'        static inline initcall_t __maybe_unused __inittest(void)                \\\n' b'                                                ^\n' b"/s/kernel/msm-5.4/drivers/firmware/qcom_scm.c:1256:1: error: redefinition of 'init_module'\n" b'early_initcall(scm_mem_protection_init);\n' b'^\n' b"/s/kernel/msm-5.4/include/linux/module.h:110:29: note: expanded from macro 'early_initcall'\n" b'#define early_initcall(fn)              module_init(fn)\n' b'                                        ^\n' b"/s/kernel/msm-5.4/include/linux/module.h:132:6: note: expanded from macro 'module_init'\n" b'        int init_module(void) __copy(initfn) __attribute__((alias(#initfn)));\n' b'            ^\n' b'/s/kernel/msm-


5.4/drivers/firmware/qcom_scm.c:1248:1: note: previous definition is here\n' b'subsys_initcall(qcom_scm_init);\n' b'^\n' b"/s/kernel/msm-5.4/include/linux/module.h:116:30: note: expanded from macro 'subsys_initcall'\n" b'#define subsys_initcall(fn)             module_init(fn)\n' b'                                        ^\n' b"/s/kernel/msm-5.4/include/linux/module.h:132:6: note: expanded from macro 'module_init'\n" b'        int init_module(void) __copy(initfn) __attribute__((alias(#initfn)));\n' b'            ^\n' b'2 errors generated.\n' make[3]: *** [/s/kernel/msm-5.4/scripts/Makefile.build:287: drivers/firmware/qcom_scm.o] Error 1
make[3]: *** Waiting for unfinished jobs....
  CC      drivers/gpu/msm/kgsl_sharedmem.o
  CC      drivers/hid/hid-logitech-dj.o


# only one initcall can be called for a module.


static int __init qcom_scm_init(void)
{
	int ret;

	ret = platform_driver_register(&qcom_scm_driver);
	if (ret)
		return ret;

	return qtee_shmbridge_driver_init();
}
subsys_initcall(qcom_scm_init);

#ifdef CONFIG_QCOM_RTIC
static int __init scm_mem_protection_init(void)
{
	return scm_mem_protection_init_do(__scm ? __scm->dev : NULL);
}

early_initcall(scm_mem_protection_init);
#endif
