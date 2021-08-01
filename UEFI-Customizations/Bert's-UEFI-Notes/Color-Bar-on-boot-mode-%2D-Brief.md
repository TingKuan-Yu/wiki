[[_TOC_]]

# Introduction

The surface duo device could show different color bars on the boot screen according to device stats. 

# The meanings of Color Bars

- Yellow Bar 
  - Indicate that the device is not fully fused.
    - xbl log: [ColorbarsDxeEndOfDxeCallback] Device is not fully fused, drawing yellow colorbar
  - Check with 
    - NOT IsProductionDevice (bits 0, 1, 2) 
    - NOT IsRpmbProvisioned (bit 5) 
    - GetDebugPolicyFlag 
    - NOT IsRollbackEnabled (bit 3) 

- Orange Bar
  - Display if device is not a production one 
  - Only check with NOT IsProductionDevice (bit 0, 1, 2) 
  - xbl log: [ColorbarsDxeEndOfDxeCallback] Device is not fused at all, drawing orange colorbar

- Green Bar 
  - The xbl image is not a ship_mode build.
  - xbl log: [ColorbarsDxeEndOfDxeCallback] SHIP_MODE is off, drawing green colorbar


- Purple Bar 
  - Display if device is in Manufacturing Mode 
  - xbl log: [ColorbarsDxeEndOfDxeCallback] - Device in Manufacturing Mode, drawing purple colorbar
  - Check with MsGetUefiRuntimeMode
  - refer to: https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/25636/Manufacturing-Mode

- Brown Bar 
  - Display if RPMB is corrupted 
  - Check with IsVolatile 

 