# boot/QcomPkg/SocPkg/Lahaina/Settings/TLMM/loader/TLMMChipset.xml
---
## DALDEVICEID_TLMM
- **tlmm_sleep**
```
<global_def>
   <var_seq name="DALTLMMBSP_LowPowerCfg" type="DALPROP_DATA_TYPE_UINT32_SEQ">
     PIN_INPUT  | PIN_PULL_DOWN | PIN_OUT_LOW | PIN_PRG_NO,
     PIN_INPUT  | PIN_PULL_DOWN | PIN_OUT_LOW | PIN_PRG_NO,
     :
     PIN_INPUT  | PIN_PULL_DOWN | PIN_OUT_LOW | PIN_PRG_NO,
     end
   </var_seq>
 </global_def>

 <device id="DALDEVICEID_TLMM">
   <props name="tlmm_sleep" type="DALPROP_ATTR_TYPE_UINT32_SEQ_PTR">
     DALTLMMBSP_LowPowerCfg
   </props>
 </device>

```

# boot/QcomPkg/SocPkg/Library/TLMMHWLib/GPIOSvcDevice.c
---
## boolean GPIO_SvcDeviceInit
-Check DALDEVICEID_TLMM & tlmm_sleep
```
 if ( bIsInitialized == FALSE )
  {
    GPIO_SyncEnter();
    
    /*
     * Initialize the properties handle.
     */
    eResult = DALSYS_GetDALPropertyHandle(DALDEVICEID_TLMM, PropsHandle.hDevice);
    
    if ( eResult == DAL_SUCCESS )
    {
        /*
       * Get the list of low-power GPIO settings.
         */
      eResult = DALSYS_GetPropertyValue( PropsHandle.hDevice, "tlmm_sleep", 0, &tPropVar );
:
```

# Building XML
---
## boot/QcomPkg/SocPkg/Lahaina/Settings/DALConfig/DALConfigLoaderLib_LA.mk
- XML_DEPS
'''
#
# Following macro i.e. XML_DEPS lists all the xml config files that
# It also enlists any xml files which are #included by other xml files.
# Any new xml file added will need to be appended to the following list.
#
XML_DEPS = $(WORKSPACE)/QcomPkg/SocPkg/Settings/BootTempCheck/boot_temp_check_props.xml \
           $(WORKSPACE)/QcomPkg/SocPkg/Lahaina/Settings/TLMM/loader/TLMMChipset.xml \
           :
'''

## boot/QcomPkg/SocPkg/Settings/devcfg/devcfg_rules.mk:
- **$(DALMOD_C)**
```
GLOBAL_DEPS = $(THISFILE) $(XML_DEPS) $(XML_XBLCONFIG_DEPS) $(INC_DEPS) $(IMAGE_CFG_XML) $(DEVCFG_SCRIPTS)/image_config.py $(DEVCFG_SCRIPTS)/propgen.py $(CALLING_MAKE_FILE)

XML_INPUT_LIST = $(addprefix -i ,$(XML_DEPS))

DALMOD_XMLS_LIST = $(XML_INPUT_LIST) $(XML_XBLCONFIG_INPUT_LIST)

$(DALMOD_C) : $(GLOBAL_DEPS)
	( python $(DEVCFG_SCRIPTS)/propgen.py -t $(DEVCFG_CONFIG) $(DALMOD_XMLS_LIST) --ModDirFile=$(DALMOD_C) -g $(IMAGE_CFG_XML) )

```
# @ TODO
- propgen.py