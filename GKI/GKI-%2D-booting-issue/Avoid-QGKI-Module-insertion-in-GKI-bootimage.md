# check uname for each boot

## QGKI
- selfhost combo
```
c1:/ # uname -a
Linux localhost 5.4.61-c1-p-2021_606_2 #1 SMP PREEMPT Sun Jun 6 16:35:57 UTC 2021 aarch64
c1:/ # cat /proc/version
Linux version 5.4.61-c1-p-2021_606_2 (user@d434f9cdabc5) (Android (7284624, based on r416183b) clang version 12.0.5 (https://android.googlesource.com/toolchain/llvm-project c935d99d7cf2016289302412d708641d52d2f7ee), LLD 12.0.5 (/buildbot/src/android/llvm-toolchain/out/llvm-project/lld c935d99d7cf2016289302412d708641d52d2f7ee)) #1 SMP PREEMPT Sun Jun 6 16:35:57 UTC 2021
```
- kernel/msm-5.4/scripts/setlocalversion
  - -c1-d or -c1-p
```
	# MSCHANGE Use custom version
	if test -z "${AZBUILDVER}"; then
		AZBUILDVER="0.0.0"
	fi
	AZBUILDVER=$(echo ${AZBUILDVER} | tr '\.' '_')

	if [ "${KERNEL_DEFCONFIG}" = "lahaina-qgki-debug_defconfig" ]
	then
		res="-c1-d-${AZBUILDVER}"
	elif [ "${KERNEL_DEFCONFIG}" = "lahaina-qgki_defconfig" ]
	then
		res="-c1-p-${AZBUILDVER}"
	elif [ "${KERNEL_DEFCONFIG}" = "lahaina-gki_defconfig" ]
	then
		res="-c1-g-${AZBUILDVER}"
	else
		#Make sure this is > 64 chars to fail the build
		res="UNKNOWN KERNEL CONFIG ${KERNEL_DEFCONFIG} - ERROR ----------------------------------------------------------------"
	fi
	# MSCHANGE End
```
- grep command
```
uname -a | grep -E "c1-d|c1-p"
```

## GKI
- null display mutli-pr
```
c1:/ $ uname -a
Linux localhost 5.4.86-c1-g-0_0_0 #2 SMP PREEMPT Mon Jun 21 06:26:19 UTC 2021 aarch64
c1:/ # cat /proc/version                                                                                                                                                                                          
Linux version 5.4.86-c1-g-0_0_0 (user@9b88b4358470) (Android (7284624, based on r416183b) clang version 12.0.5 (https://android.googlesource.com/toolchain/llvm-project c935d99d7cf2016289302412d708641d52d2f7ee), LLD 12.0.5 (/buildbot/src/android/llvm-toolchain/out/llvm-project/lld c935d99d7cf2016289302412d708641d52d2f7ee)) #2 SMP PREEMPT Mon Jun 21 06:26:19 UTC 2021
```
- gki signed-aosp_arm64-img-7111047
```
c1:/ # uname -a
Linux localhost 5.4.61-android11-2-00020-g68ecddcda842-ab7092597 #1 SMP PREEMPT Tue Jan 19 19:02:47 UTC 2021 aarch64
c1:/ # cat /proc/version
Linux version 5.4.61-android11-2-00020-g68ecddcda842-ab7092597 (build-user@build-host) (Android (6443078 based on r383902) clang version 11.0.1 (https://android.googlesource.com/toolchain/llvm-project b397f81060ce6d701042b782172ed13bee898b79), LLD 11.0.1 (/buildbot/tmp/tmp6_m7QH b397f81060ce6d701042b782172ed13bee898b79)) #1 SMP PREEMPT Tue Jan 19 19:02:47 UTC 2021
```

- hi202 boot-debug-gki.img
```
c1:/ # uname -a
Linux localhost 5.4.61-00002-g6513445841c4-dirty #10 SMP PREEMPT Sun Jun 6 13:23:39 CST 2021 aarch64
c1:/ # cat /proc/version
Linux version 5.4.61-00002-g6513445841c4-dirty (tingkuanyu@TonyYuLinux1) (Android (6443078 based on r383902) clang version 11.0.1 (https://android.googlesource.com/toolchain/llvm-project b397f81060ce6d701042b782172ed13bee898b79), LLD 11.0.1 (/buildbot/tmp/tmp6_m7QH b397f81060ce6d701042b782172ed13bee898b79)) #10 SMP PREEMPT Sun Jun 6 13:23:39 CST 2021
```