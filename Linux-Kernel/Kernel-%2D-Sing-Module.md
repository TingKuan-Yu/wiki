# kernel/msm-5.4/Documentation/admin-guide/module-signing.rst
- automatically signed during the **modules_install** phase of a build
```
   (``CONFIG_MODULE_SIG_ALL``)
     If this is on then modules will be automatically signed during the
     modules_install phase of a build.  If this is off, then the modules must
     be signed manually using::

	scripts/sign-file
```

# kernel/msm-5.4/Makefile
- modules_install target
```
PHONY += modules_install
modules_install: _emodinst_ _emodinst_post

install-dir := $(if $(INSTALL_MOD_DIR),$(INSTALL_MOD_DIR),extra)
PHONY += _emodinst_
_emodinst_:
	$(Q)mkdir -p $(MODLIB)/$(install-dir)
	$(Q)$(MAKE) -f $(srctree)/scripts/Makefile.modins

```

# kernel/msm-5.4/scripts/Makefile.modsign
- $(call cmd,sign_ko,$(MODLIB)/$(modinst_dir))
  - call cmd_sign_ko to sign module
```
        cmd_sign_ko = $(mod_sign_cmd) $(2)/$(notdir $@)

# Modules built outside the kernel source tree go into extra by default
INSTALL_MOD_DIR ?= extra
ext-mod-dir = $(INSTALL_MOD_DIR)$(subst $(patsubst %/,%,$(KBUILD_EXTMOD)),,$(@D))

modinst_dir = $(if $(KBUILD_EXTMOD),$(ext-mod-dir),kernel/$(@D))

$(modules):
	$(call cmd,sign_ko,$(MODLIB)/$(modinst_dir))
```

# kernel/msm-5.4/scripts/Kbuild.include
```
# echo command.
# Short version is used, if $(quiet) equals `quiet_', otherwise full one.
echo-cmd = $(if $($(quiet)cmd_$(1)),\
	echo '  $(call escsq,$($(quiet)cmd_$(1)))$(echo-why)';)

# printing commands
cmd = @set -e; $(echo-cmd) $(cmd_$(1))

```

# Bug 146287: [QC 05188529][msm_drm /dlkm] Recovery screen does not show up in selfhost builds
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/146287/
- PRs to boot into fastbootd and recovery mode.
  - 1.  your patch
https://dev.azure.com/E-OS/device/_git/caf-platform.vendor.opensource.display-drivers/pullrequest/27893
  - 2. Fix bug for failed handling vendor_ramdisk_modules.zip
https://dev.azure.com/E-OS/device/_git/caf-kernel.build/pullrequest/27892
  - 3. Add ko in kernel.json
https://dev.azure.com/E-OS/device/_git/device.config/pullrequest/27891

- Multi-pr is building. 
  - QGKI - debug: 
I just tested it, it is bootable. Adb reboot fastboot also works.
https://dev.azure.com/E-OS/device/_build/results?buildId=741086&view=results
  - QGKI - user
https://dev.azure.com/E-OS/device/_build/results?buildId=741088&view=results
  - GKI - user
https://dev.azure.com/E-OS/device/_build/results?buildId=741089&view=results

