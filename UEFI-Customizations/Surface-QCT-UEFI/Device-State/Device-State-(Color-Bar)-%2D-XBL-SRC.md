# Device state related files
- boot/Sm8350FamilyPkg/Include/Library/
  - DeviceStateLib.h
- boot/Sm8350FamilyPkg/Library/ColorBarDisplayDeviceStateLib/
  - ColorBarDisplayDeviceStateLib.c


# boot/Sm8350FamilyPkg/Include/Library/
## boot/Sm8350FamilyPkg/Include/Library/DeviceStateLib.h
- The types of device state
  - DEVICE_STATE_DEVELOPMENT_BUILD_ENABLED
    - set 1 for not a SHIP_MODE build
```
#define DEVICE_STATE_SECUREBOOT_OFF            (1 << (0))
#define DEVICE_STATE_MANUFACTURING_MODE        (1 << (1))
#define DEVICE_STATE_DEVELOPMENT_BUILD_ENABLED (1 << (2))
#define DEVICE_STATE_SOURCE_DEBUG_ENABLED      (1 << (3))
#define DEVICE_STATE_UNDEFINED                 (1 << (4))
#define DEVICE_STATE_UNIT_TEST_MODE            (1 << (5))

#define DEVICE_STATE_PLATFORM_MODE_0           (1 << (24))
#define DEVICE_STATE_PLATFORM_MODE_1           (1 << (25))
#define DEVICE_STATE_PLATFORM_MODE_2           (1 << (26))
#define DEVICE_STATE_PLATFORM_MODE_3           (1 << (27))

#define DEVICE_STATE_MAX                       (1 << (31))
```
- type definition of device state
```
typedef UINT32  DEVICE_STATE;
```

# boot/Sm8350FamilyPkg/Library/ColorBarDisplayDeviceStateLib/
## boot/Sm8350FamilyPkg/Library/ColorBarDisplayDeviceStateLib/ColorBarDisplayDeviceStateLib.c
```
//
// List of supported notifications.
// In order you want them displayed.
//
DEVICE_STATE mSupportedNotifications[] = {
  (DEVICE_STATE)DEVICE_STATE_SECUREBOOT_OFF,
  (DEVICE_STATE)DEVICE_STATE_PLATFORM_MODE_0,
  (DEVICE_STATE)DEVICE_STATE_PLATFORM_MODE_1,
  (DEVICE_STATE)DEVICE_STATE_PLATFORM_MODE_2,
  (DEVICE_STATE)DEVICE_STATE_PLATFORM_MODE_3,
  (DEVICE_STATE)DEVICE_STATE_DEVELOPMENT_BUILD_ENABLED,
  (DEVICE_STATE)DEVICE_STATE_SOURCE_DEBUG_ENABLED,
  (DEVICE_STATE)DEVICE_STATE_MANUFACTURING_MODE,
  (DEVICE_STATE)DEVICE_STATE_UNIT_TEST_MODE,

  (DEVICE_STATE)DEVICE_STATE_MAX  //this needs to be the last one
};
/**
Function to Display all Active Device States

@param FrameBufferBase   - Address of point 0,0 in the frame buffer
@param PixelsPerScanLine - Number of pixels per scan line.
@param WidthInPixels     - Number of Columns in FrameBuffer
@param HeightInPixels    - Number of Rows in FrameBuffer
**/
VOID
EFIAPI
DisplayDeviceState(
IN  UINT8* FrameBufferBase,
IN  INT32  PixelsPerScanLine,
IN  INT32  WidthInPixels,
IN  INT32  HeightInPixels
)
{
  DEVICE_STATE Notifications = 0;
  DEVICE_STATE* SupportedNotification = mSupportedNotifications;
:
}
```