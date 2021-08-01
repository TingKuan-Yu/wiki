# build/make/core/root.mk
```
include build/make/core/config.mk
include build/make/core/main.mk
```

# hlos_vendor/build/make/core/main.mk
- **Makefile**
```
include $(BUILD_SYSTEM)/Makefile
```

# build/make/core/config.mk
```
include $(BUILD_SYSTEM)/envsetup.mk
```

# hlos_vendor/build/make/core/envsetup.mk
```
include $(BUILD_SYSTEM)/board_config.mk
```

# hlos_vendor/build/make/core/Makefile
- include
```
-include $(sort $(wildcard vendor/*/build/tasks/*.mk))
-include $(sort $(wildcard device/*/build/tasks/*.mk))
-include $(sort $(wildcard product/*/build/tasks/*.mk))
-include $(sort $(wildcard vendor/*/*/build/tasks/*.mk))
-include $(sort $(wildcard device/*/*/build/tasks/*.mk))
-include $(sort $(wildcard product/*/*/build/tasks/*.mk))
include $(sort $(wildcard platform_testing/build/tasks/*.mk))
include $(sort $(wildcard test/vts/tools/build/tasks/*.mk))
```
- generate_extra_images.mk
```
tingkuanyu@TonyYuLinux1:/E/GKI/hlos_vendor$ ls vendor/*/build/tasks/*.mk
vendor/qcom/build/tasks/generate_extra_images.mk   vendor/qcom/build/tasks/qcv_checker.mk       vendor/qcom/build/tasks/QSSI_violators.mk
vendor/qcom/build/tasks/generate_vendor_bundle.mk  vendor/qcom/build/tasks/QMAA_enforcement.mk  vendor/qcom/build/tasks/vendor_prop_context_restriction.mk

tingkuanyu@TonyYuLinux1:/E/GKI/hlos_vendor$ ls -al vendor/qcom/build/tasks/generate_extra_images.mk
lrwxrwxrwx 1 tingkuanyu tingkuanyu 55 Jun 15 13:50 vendor/qcom/build/tasks/generate_extra_images.mk -> ../../../../device/qcom/common/generate_extra_images.mk
```