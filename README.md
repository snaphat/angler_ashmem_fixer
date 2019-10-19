# angler_ashmem_fixer

## About
A [Magisk](https://magiskmanager.com) module that fixes missing ashmem libraries used by com.android.media* on the Nexus 6p running the Android 10 Pixel Experience Rom. These are included with the rom but not in the path.
  
## Installation
  * Install the ashmem_fixer.zip via Magisk Manager.
  
## Clone:
```
git clone git@github.com:snaphat/angler_ashmem_fixer.git
```

## Technical Explanation
The current build of the Pixel Experience 10 rom contains a bug that causes com.android.media* to crash when Android Shared memory is requested. The log of this error is shown below: 
```
10-18 20:25:00.781   599 32692 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:25:00.782   599 32692 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:25:00.799   599 16329 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:09.734   599  3331 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:09.735   599  3331 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:09.764   599 16566 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:22.148   599  3331 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:22.148   599  3331 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
10-18 20:59:22.167   599 16650 E ashmem  : Failed to dlopen() libashmemd_client.so: dlopen failed: library "libashmemd_client.so" not found
```

It's simply due to the ```libashmemd_client.so``` and ```ashmemd_aidl_interface-cpp.so``` libraries being missing underneathe of ```/system/apex/com.android.media/lib64``` and ```/system/apex/com.android.media.swcodec/lib64```. This module just copies them over on boot.
