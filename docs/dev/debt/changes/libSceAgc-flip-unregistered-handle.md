# libSceAgc

## add Unknown function info

- [sceAgcDcbSetFlip, sceAgcAcbSetFlip, sceAgcDcbWaitUntilSafeForRendering, sceAgcAcbWaitUntilSafeForRendering](../../../core/libs/prx/libSceAgc/DcbState/src/Display.cpp) (libSceAgc) - prosper's console measurements (`agcbuild` family) show all four returning null and leaving the command buffer untouched for handles `0x11111111`, `1` and `0x22222222` with no video output open. AnyPS5 now returns null without writing when the handle is not registered with the driver by `sceVideoOutOpen`, and still throws for a null buffer. Which check the console makes is not measured: it may reject the handle, the display buffer index, or the flip mode, and its answer for an open handle with an out-of-range index or mode is unknown.
