# Custom NVIDIA 390x Driver for P106-100 + Legacy GPU Setup

## Overview

This custom NVIDIA 390x driver enables simultaneous operation of P106-100 mining cards alongside legacy GPUs (like GT 610) for display output. Designed for systems without integrated graphics or where you need a dedicated display adapter while utilizing P106-100 for compute workloads.

## Why This Driver?

- **No integrated graphics** in your CPU
- **P106-100 has no display outputs** (mining card limitation)
- **Need legacy GPU for display** while P106-100 handles compute tasks
- **Standard drivers don't support** this mixed configuration properly

## Supported Hardware

### Primary Compute GPU
- **NVIDIA P106-100** (all variants)
  - 3GB and 6GB models
  - All manufacturers (MSI, ASUS, Gigabyte, etc.)

### Display GPU (Required for video output)
- **GT 610** (tested)
- **GT 710**
- **GT 730**
- **GTX 750/750 Ti**
- Other legacy NVIDIA cards from 400-1000 series

## System Requirements

- **OS**: Windows 10/11 (64-bit)
- **CPU**: Any without integrated graphics OR integrated graphics disabled
- **PSU**: Sufficient power for both cards
- **Motherboard**: Multiple PCIe slots

## Installation Guide

### Step 1: Prepare System

1. **Remove existing NVIDIA drivers**
   ```
   Download DDU (Display Driver Uninstaller)
   Boot to Safe Mode
   Run DDU with "Clean and Restart" option
   ```

2. **Disable Driver Signature Enforcement**
   ```
   Press Win + R
   Type: shutdown /r /o /t 0
   Press Enter
   
   After restart:
   Troubleshoot > Advanced Options > Startup Settings > Restart
   Press F7 - "Disable driver signature enforcement"
   ```

### Step 2: Hardware Setup

1. **Install both GPUs**
   - P106-100 in primary PCIe x16 slot
   - GT 610 (or other legacy GPU) in secondary slot
   
2. **Connect display cables**
   - **IMPORTANT**: Connect monitor to GT 610, NOT P106-100
   - P106-100 has no display outputs

3. **Power connections**
   - Ensure both cards have adequate power
   - P106-100 typically needs 6-pin PCIe power

### Step 3: Driver Installation

1. **Download driver package**
   - Extract to temporary folder (e.g., C:\NVIDIA_Custom)

2. **Install as Administrator**
   - Right-click installer → "Run as administrator"
   - Choose "Custom Installation"
   - Select "Perform clean installation"
   - Complete installation

3. **Restart system** (Required)
   - System will restart automatically
   - **May require 2-3 restarts** for full recognition

### Step 4: Verification

1. **Check Device Manager**
   - Both GPUs should appear under "Display adapters"
   - No yellow warning triangles

2. **NVIDIA Control Panel**
   - Should detect both cards
   - GT 610 handles display
   - P106-100 available for compute

## Configuration

### GPU Roles
- **GT 610**: Primary display adapter, Windows desktop, basic graphics
- **P106-100**: Compute tasks, mining, CUDA applications, rendering

### NVIDIA Control Panel Settings
1. Open NVIDIA Control Panel
2. "Manage 3D settings" → "Program Settings"
3. For mining software: Select P106-100
4. For desktop/games: Use GT 610 or auto-select

## Common Issues & Solutions

### Issue: "Unsigned driver" installation error
**Solution:**
- Ensure signature enforcement is disabled
- Restart in test mode: `bcdedit /set testsigning on`
- Reboot and try installation again

### Issue: P106-100 not detected
**Solution:**
- Check PCIe power connections
- Verify PSU wattage (P106-100 needs ~120W)
- Try different PCIe slot
- Restart system multiple times

### Issue: No display output
**Solution:**
- **Critical**: Connect monitor to GT 610, not P106-100
- P106-100 mining cards have no video outputs
- Ensure GT 610 is properly seated

### Issue: System crashes/instability
**Solution:**
- Check PSU capacity (recommend 650W+ for this setup)
- Verify RAM compatibility
- Install cards one at a time to isolate issues

### Issue: Mining software doesn't see P106-100
**Solution:**
- Update mining software to latest version
- Manually select GPU in miner settings
- Check CUDA installation

## Advanced Configuration

### For CUDA Development
```
Install CUDA toolkit
Set P106-100 as CUDA device
GT 610 remains display adapter
```

### Registry Tweaks (Advanced)
If experiencing detection issues:
```
Open regedit as administrator
Navigate to: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}
Find NVIDIA entries
Add DWORD: EnableMSHybrid = 0
```

## Performance Tips

1. **Power Settings**
   - Windows: High Performance mode
   - NVIDIA: Prefer Maximum Performance

2. **Memory Management**
   - 8 GB RAM recommended for dual-GPU setup
   - Monitor GPU memory usage

3. **Cooling**
   - Ensure adequate case ventilation
   - P106-100 can run hot under load

## Compatibility

### Tested Working Configurations
- P106-100 6GB + GT 610 2GB
- P106-100 3GB + GT 710 1GB  
- P106-100 6GB + GT 730 2GB
- P106-100 6GB + GTX 750 Ti 2GB

### Software Compatibility
- **CUDA**: CUDA 11.x and older
- **Games**: Limited (use GT 610 for display)
- **Rendering**: Blender, DaVinci Resolve

## Troubleshooting Checklist

Before asking for help:
- [ ] Both GPUs detected in Device Manager
- [ ] Monitor connected to GT 610 (not P106-100)
- [ ] Driver signature enforcement disabled
- [ ] System restarted multiple times
- [ ] PSU has adequate wattage
- [ ] Latest mining software installed

## Important Notes

- **This driver is UNSIGNED** - requires disabled signature enforcement
- **Windows only** - no Linux support
- **Restart required** - sometimes multiple restarts needed
- **GT 610 for display** - P106-100 has no video outputs
- **Mining focused** - not optimized for gaming

## Support

For issues:
1. Check existing [Issues](../../issues)
2. Provide complete system specs
3. Include error messages/screenshots
4. List both GPU models and manufacturers

## Disclaimer

This modified driver is provided as-is. Use at your own risk. Always backup your system before installation. Not affiliated with NVIDIA.

---
**Driver Version**: 390.x Custom  
**Target Use**: P106-100 + Legacy GPU Display  
**Platform**: Windows 10/11 64-bit
