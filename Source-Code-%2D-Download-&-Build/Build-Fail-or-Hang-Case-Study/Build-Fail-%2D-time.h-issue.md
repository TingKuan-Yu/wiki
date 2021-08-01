# log
```
In file included from ./usr/include/display/media/msm_sde_rotator.h:9:
./usr/include/linux/videodev2.h:2313:8: error: redefinition of 'timespec'
struct timespec {
       ^
/usr/include/time.h:120:8: note: previous definition is here
struct timespec
       ^
```

# fix 
```
- #include <sys/time.h>
+ #include <linux/time.h>
```