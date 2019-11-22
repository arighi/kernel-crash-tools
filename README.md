# kernel-crash-tools

Simple wrappers around qemu/crash to speed up kernel development

Run these tools from a kernel build directory to test, generate a crash dump
and analyze it.

Required tools / packages:
  - qemu
  - crash
  - virtme

# Example
```
 $ cd src/linux
 $ kernel-test
 ...
 virtme-init: console is ttyS0
 root@(none):/#
```

On another console session run kernel-dump to generate a crash dump:
```
 $ cd src/linux
 $ kernel-dump /tmp/vmcore.img
 ...

```

Analyze the crash dump:
```
 $ kernel-show /tmp/vmcore.img
 ...

 crash> bt
 PID: 0      TASK: ffffffff8261b800  CPU: 0   COMMAND: "swapper/0"
     [exception RIP: native_safe_halt+14]
     RIP: ffffffff81ba96ce  RSP: ffffffff82603e10  RFLAGS: 00000206
     RAX: ffffffff8261b800  RBX: 0000000000000000  RCX: 0000000000000000
     RDX: ffffffff8261b800  RSI: 0000000000000006  RDI: ffffffff8261b800
     RBP: ffffffff82603e30   R8: 0000000000000001   R9: 0000000000000000
     R10: 0000000000000000  R11: 0000000000000000  R12: 0000000000000000
     R13: ffffffff8261b800  R14: 0000000000000000  R15: 0000000000000000
     CS: 0010  SS: 0018
  #0 [ffffffff82603e10] default_idle at ffffffff81ba92b5
  #1 [ffffffff82603e38] arch_cpu_idle at ffffffff81040685
  #2 [ffffffff82603e48] default_idle_call at ffffffff81ba9893
  #3 [ffffffff82603e58] do_idle at ffffffff810db810
  #4 [ffffffff82603eb0] cpu_startup_entry at ffffffff810dbb30
  #5 [ffffffff82603ec8] rest_init at ffffffff81b994aa
  #6 [ffffffff82603ee0] arch_call_rest_init at ffffffff82b42c9d
  #7 [ffffffff82603ef0] start_kernel at ffffffff82b43209
  #8 [ffffffff82603f28] x86_64_start_reservations at ffffffff82b4244c
  #9 [ffffffff82603f38] x86_64_start_kernel at ffffffff82b424c5
 #10 [ffffffff82603f50] secondary_startup_64 at ffffffff810000d4
```

NOTE: all the commands above should be executed from the kernel build directory
(with a compiled vmlinux and all object files present).

# See also
- virtme:
  https://github.com/amluto/virtme

- blog post about virtme:
  http://arighi.blogspot.com/2019/08/kerneldebuggingusingqemu.html
