Background Geolocation for iOS

used by:

* [react-native-background-geolocation](https://github.com/mauron85/react-native-background-geolocation)

* [cordova-plugin-background-geolocation](https://github.com/mauron85/cordova-plugin-background-geolocation)

# Building a single "fat" static library for device + simulator

See:

* [Build fat static library (device + simulator) using Xcode and SDK 4+](https://stackoverflow.com/questions/3520977/build-fat-static-library-device-simulator-using-xcode-and-sdk-4)

However, the trick is to then select the Generic iOS Device target, otherwise it will only generate code for armv7 and arm64

You can inspect which targets are included in the library by using:

```
lipo -detailed_info BackgroundGeolocation.a 
```

If correctly built, the output should be:

```
Fat header in: BackgroundGeolocation.a
fat_magic 0xcafebabe
nfat_arch 4
architecture armv7
    cputype CPU_TYPE_ARM
    cpusubtype CPU_SUBTYPE_ARM_V7
    offset 88
    size 2254248
    align 2^2 (4)
architecture i386
    cputype CPU_TYPE_I386
    cpusubtype CPU_SUBTYPE_I386_ALL
    offset 2254336
    size 2145960
    align 2^2 (4)
architecture x86_64
    cputype CPU_TYPE_X86_64
    cpusubtype CPU_SUBTYPE_X86_64_ALL
    offset 4400296
    size 2144624
    align 2^3 (8)
architecture arm64
    cputype CPU_TYPE_ARM64
    cpusubtype CPU_SUBTYPE_ARM64_ALL
    offset 6544920
    size 2498320
    align 2^3 (8)
```

To find the correct generated library look in:

$HOME/Library/Developer/Xcode/DerivedData/BackgroundGeolocation-<gobbledegook>/Build/Products/Debug-universal
