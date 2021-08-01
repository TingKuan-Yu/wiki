1. Readonly variable can't be define in BoardConfig.mk
- refer to build/make/core/product.mk
```
#
# Mark the variables in _product_stash_var_list as readonly
#
define readonly-variables
$(foreach v,$(1), \
  $(eval $(v) ?=) \
  $(eval .KATI_READONLY := $(v)) \
 )
endef
```