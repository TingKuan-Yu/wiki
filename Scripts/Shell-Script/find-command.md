find $$(PRIVATE_MODULE_DIR) -type f -name *.ko -exec ls -1rt "{}" + | xargs basename -a > $$(PRIVATE_LOAD_FILE); 
- find -exec