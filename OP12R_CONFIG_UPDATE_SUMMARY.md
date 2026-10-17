# OP12R.json Configuration Update Summary for Android 16 Target

## Current Configuration (android13/kernel 5.15)
```json
{
  "model": "OP12R",
  "product": "OnePlus 12R 5G",
  "soc": "kalama",
  "codename": "aston",
  "branch": "oneplus/sm8550",
  "boot_partition_size": "201326592",
  "vendor_boot_partition_size": "201326592",
  "qcacld_dev_name": "kiwi_v2",
  "clang": "manifest",
  "tree": "mixed",
  "manifest_oos15": {
    "url": "https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_v.xml",
    "os": "OxygenOS 15",
    "os_short": "oos15"
  },
  "manifest_oos16": {
    "url": "https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b.xml",
    "os": "OxygenOS 16",
    "os_short": "oos16"
  },
  "manifest_oos16_custom": {
    "url": " https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b_custom.xml",
    "os": "OxygenOS 16",
    "os_short": "oos16"
  },
  "android_version": "android13",
  "kernel_version": "5.15",
  "hmbird": false
}
```

## Required Changes for Android 16 Target (android14/kernel 6.1)
```diff
{
  "model": "OP12R",
  "product": "OnePlus 12R 5G",
  "soc": "kalama",
  "codename": "aston",
  "branch": "oneplus/sm8550",
  "boot_partition_size": "201326592",
  "vendor_boot_partition_size": "201326592",
  "qcacld_dev_name": "kiwi_v2",
  "clang": "manifest",
  "tree": "mixed",
  "manifest_oos15": {
    "url": "https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_v.xml",
    "os": "OxygenOS 15",
    "os_short": "oos15"
  },
  "manifest_oos16": {
    "url": "https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b.xml",
    "os": "OxygenOS 16",
    "os_short": "oos16"
  },
  "manifest_oos16_custom": {
    "url": " https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b_custom.xml",
    "os": "OxygenOS 16",
    "os_short": "oos16"
  },
-   "android_version": "android13",
-   "kernel_version": "5.15",
+   "android_version": "android14",
+   "kernel_version": "6.1",
  "hmbird": false
}
```

## Rationale for Changes

1. **android_version: android13 → android14**
   - Android 16 target requires Android 14 as the AOSP base (following established pattern)
   - Matches OP12 configuration which targets Android 16 devices
   - The "android14" value represents the AOSP version upon which Android 16 is built

2. **kernel_version: 5.15 → 6.1**
   - Android 16 with GKI 2.0 requires Linux kernel 6.1
   - Matches OP12 configuration which uses kernel 6.1 for Android 16 target
   - GKI 2.0 is specifically designed to work with kernel 6.1 LTS

## Verification Points After Update

1. **Manifest Accessibility**: Verify that the OxygenOS 16 manifest URLs are accessible:
   - https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b.xml
   - https://raw.githubusercontent.com/nullptr-t-oss/kernel_kit/refs/heads/main/kernel_manifest/oneplus/oneplus_12r_b_custom.xml

2. **Branch Validity**: Confirm that "oneplus/sm8550" branch exists in the kernel manifest source

3. **Build Testing**: 
   - Select OP12R model in workflow
   - Select "oos16" or "oos16_custom" manifest
   - Verify build completes successfully
   - Verify resulting boot.img and vendor_boot.img have correct sizes

4. **Feature Validation**:
   - Confirm KernelSU-Next compatibility
   - Confirm SUSFS compatibility  
   - Confirm NetHunter features work
   - Confirm USB Wi-Fi driver support (qcacld-3.0 with kiwi_v2)

## Safety Notes

- This change follows the exact same pattern as the OP12 (OnePlus 12) configuration
- Only updates the version fields - all device-specific identifiers remain correct
- No changes to SoC, codename, partition sizes, or manifest structure
- Reversible if issues are discovered (can revert to android13/5.15)
- Does not affect other device configurations in the repository