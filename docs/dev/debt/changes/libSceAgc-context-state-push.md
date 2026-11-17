# libSceAgc

## change [sceAgcDcbContextStateOp](../../../core/libs/prx/libSceAgc/DcbState/src/ContextState.cpp)

- [sceAgcDcbContextStateOp](../../../core/libs/prx/libSceAgc/DcbState/src/ContextState.cpp) (libSceAgc) - operation 1 writes the console's `CONTEXT_CONTROL` (load 0, shadow `0x80018001`) and `CLEAR_STATE` 1 and returns the first packet, as measured by `agcbuild_DcbContextStateOp_b`; `sceAgcDcbContextStateOpGetSize(1)` still reports KytyPS5's 108 bytes, more than the 20 written. Operations 0, 2 and 3 delegate to `sceAgcDcbContextStateOp_0100` (same packets as KytyPS5's `AgcDcbContextStateOp`) and were not compared with a real console. For operations above 3 the console writes only `CLEAR_STATE` with the low bits of the operation and returns null (`_a`, `_c`: 1 and 2, which do not tell a 2-bit from a 4-bit mask); here it throws

# libSceAgcDriver

## add Functional

- [CLEAR_STATE commands and CONTEXT_CONTROL shadowing](../../../core/libs/prx/libSceAgcDriver/Execution/src/Pm4.cpp) (libSceAgcDriver, opcodes 0x12 and 0x28) - `CLEAR_STATE` command 0 clears the context, 1 pushes it, 2 pops it and 3 pushes and clears it, as the `CONTEXT_STATE` NOP operations do. That reading is inferred, not measured: the console's `sceAgcDcbContextStateOp(1)`, which AnyPS5 runs as a push, writes `CLEAR_STATE` 1 (`agcbuild_DcbContextStateOp_b`). Commands 4 to 15 are refused. `CONTEXT_CONTROL` accepts the shadow-control word `0x80018001` that packet carries and keeps no shadow memory, since no load is requested
