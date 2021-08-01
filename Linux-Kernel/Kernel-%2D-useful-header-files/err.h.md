# kernel/msm-5.4/include/linux/err.h

## IS_ERR_VALUE(x)
- (unsigned long)-MAX_ERRNO --> a big vaule because force unsigned long
```
#define MAX_ERRNO	4095
#define IS_ERR_VALUE(x) unlikely((unsigned long)(void *)(x) >= (unsigned long)-MAX_ERRNO)
```
## IS_ERR()
- if ptr is a very big unsgined log number, return true
```
static inline bool __must_check IS_ERR(__force const void *ptr)
{
	return IS_ERR_VALUE((unsigned long)ptr);
}
```

## IS_ERR_OR_NULL()
- return true if error or null
```
static inline bool __must_check IS_ERR_OR_NULL(__force const void *ptr)
{
	return unlikely(!ptr) || IS_ERR_VALUE((unsigned long)ptr);
}
```