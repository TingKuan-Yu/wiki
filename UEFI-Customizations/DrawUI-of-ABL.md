
# Introduction
  There are some modification in ABL to make UI colorful for UI of ABL stage. This page show the howto. Please note that the path of files described in this page are base on abl/bootable/bootloader/edk2/QcomModulePkg.

# Color definition
- Include/Library/DrawUI.h
typedef enum {
  BGR_WHITE,
  BGR_BLACK,
  BGR_ORANGE,
  BGR_YELLOW,
  BGR_RED,
  BGR_GREEN,
  BGR_BLUE,
  BGR_CYAN,
  BGR_SILVER,
  BGR_BLACK_TEXT,
} COLOR_TYPE;


# Method modification

- Library/BootLib/DrawUI.c
STATIC EFI_GRAPHICS_OUTPUT_BLT_PIXEL mColors[] = {
        [BGR_WHITE]  = {0xff, 0xff, 0xff, 0x00},
        [BGR_BLACK]  = {0x00, 0x00, 0x00, 0x00},
        [BGR_ORANGE] = {   3,  108,  255,    0},
        [BGR_YELLOW] = {0x00, 0xff, 0xff, 0x00},
        [BGR_RED]    = {0x00, 0x00, 0x98, 0x00},
        [BGR_GREEN]  = {0x00, 0xff, 0x00, 0x00},
        [BGR_BLUE]   = { 255,  205,    5, 0x00},
        [BGR_CYAN]   = { 255,  205,    5, 0x00},
        [BGR_SILVER] = {0xc0, 0xc0, 0xc0, 0x00},
        [BGR_BLACK_TEXT] = {0x01, 0x01, 0x01, 0x00},
};
