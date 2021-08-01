# BOOT.MXF.1.0/boot_images/boot/QcomPkg/LoaderFramework/Include/boot_config.h
---
## source
```
/**
 * Boot configuration table entry 
 */
typedef struct
{
  boot_media_type media_type;             /**< Media type / MediaInterface to use when loading */
  secboot_sw_type target_img_sec_type;    /**< Secure Software ID of the target */
  config_image_type config_img_type;      /**< Type of image to be loaded */
  boot_elf_loader_sync_type elf_sync_type;/**< Load and Hash type */
  boot_boolean optional_image;            /**< Target is an optional image */
  boot_boolean load;                      /**< Target will be loaded */
  boot_boolean auth;                      /**< Target will be authenticated */
  boot_boolean exec;                      /**< Target will execute immediately after
                                               loading/authentication */
  boot_boolean jump;                      /**< Target will be jumped to after
                                               post procedures are complete */ 
  boot_procedure_func_type exec_func;     /**< Function pointer to execute function.
                                               Must be defined if exec is TRUE */ 
  boot_procedure_func_type jump_func;     /**< Function pointer to jump function.
                                               Must be defined if jump is TRUE */ 
  boot_function_table_type *pre_procs;    /**< Function pointer array to pre-procedures */
  boot_function_table_type *post_procs;   /**< Function pointer array to post-procedures */
  boot_logical_func_type load_cancel_func;/**< Function pointer to cancel loading */
  boot_load_metadata_func_type load_metadata_func;   /**< Function to load metadata for the image */
  uint8 * target_img_partition_id;        /**< Target image partition ID information */
  uint64 seg_elf_entry_point;             /**< Entry point for segmented ELF */
  ram_partition_type_t ram_part_entry_type;     /**< Attributes for RAM partition table type */
  whitelst_tbl_entry_type *whitelist_ptr;  /**< ptr to the image whitelist table */
  uint32 whitelist_num_valid_entries;         /**< number of valid entries in whitelist */
  uint8 * target_img_str;                 /**< Target image name information  */
  boot_boolean config_context_open;       /**< Create a separate config copntext object and keep it alive */
  uint32 RESERVED_4;                      /**< RESERVED */
} boot_configuration_table_entry;
```
##  boot_function_table_type *pre_procs;    /**< Function pointer array to pre-procedures */

##  boot_function_table_type *post_procs;   /**< Function pointer array to post-procedures */

##  boot_logical_func_type load_cancel_func;/**< Function pointer to cancel loading */

# BOOT.MXF.1.0/boot_images/boot/QcomPkg/LoaderFramework/ConfigContext/boot_process_config_context.c
---
