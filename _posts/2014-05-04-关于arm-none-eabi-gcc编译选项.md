---
layout : post
title : 关于arm-none-eabi-gcc编译选项]
tag : ARM GCC
---

3.17.4 ARM Options

These ‘-m’ options are defined for Advanced RISC Machines (ARM) architectures:
这些“-m” 选项是为了Advanced RISC Machines(ARM)架构定义的。

* -mabi=name
    为特定的二进制文件接口所生成的代码。可能的值有：“apcs-gun”，“atpcs”，“aapcs”，
    “aapcs-linux”和“iwmmxt”。

    Generate code for the specified ABI. Permissible values are: ‘apcs-gnu’, 
    ‘atpcs’, ‘aapcs’, ‘aapcs-linux’ and ‘iwmmxt’.

* -mapcs-frame
    为所有函数生成一个堆栈架构去兼容ARM过程调用标准（aapcs），即使这不是必须严格
    正确执行的代码。参数 *-fomit-frame-pointer* 和本参数一起使用可以使叶子函数不
    生成这个堆栈架构。默认值是 *-mno-apcs-frame* 。

    Generate a stack frame that is compliant with the ARM Procedure Call 
    Standard for all functions, even if this is not strictly necessary for correct 
    execution of the code. Specifying -fomit-frame-pointer with this option causes 
    the stack frames not to be generated for leaf functions. The default is 
    -mno-apcs-frame.

* -mapcs
    这个和 *-mapcs-frame* 参数相同。

    This is a synonym for -mapcs-frame.

* -mthumb-interwork
    生成的代码支持在ARM指令集和Thumb指令集之中调用指令。没有这个参数时，在pre-V5架构
    中，两种指令集不能可靠的用于一个程序中。默认值是 *-mno-thumb-interwork* ，当生成
    稍大些的代码时，参数 *-mthumb-interwork* 会被设定。在AAPCS被设定时，这个选项是没
    有意义的。

    Generate code that supports calling between the ARM and Thumb instruction 
    sets. Without this option, on pre-v5 architectures, the two instruction sets 
    cannot be reliably used inside one program. The default is -mno-thumb-interwork, 
    since slightly larger code is generated when -mthumb-interwork is specified. In 
    AAPCS configurations this option is meaningless.

* -mno-sched-prolog
     
    Prevent the reordering of instructions in the function prologue, or the 
    merging of those instruction with the instructions in the function's body. This 
    means that all functions start with a recognizable set of instructions (or in 
    fact one of a choice from a small set of different function prologues), and this 
    information can be used to locate the start of functions inside an executable 
    piece of code. The default is -msched-prolog.

* -mfloat-abi=name
    指定使用哪个浮点数二进制文件接口。可能的值有：“soft”，“softfp”，“hard”。

    当值为“soft”时，GCC生成包含输出库的浮点数操作。
    当值为“softfp”时，生成的代码允许使用硬件浮点指令，但是仍使用软件浮点调用约定。
    当值为“hard”时，生成的代码允许使用硬件浮点指令，且使用硬件浮点处理器指定的调用约定。

    默认值取决于具体的目标配置。注意硬件浮点和软件浮点的ABI是链接不兼容的。所以必须编译
    具有相同的ABI的程序，并使用兼容的库链接。

    Specifies which floating-point ABI to use. Permissible values are: ‘soft’, 
‘softfp’ and ‘hard’.

    Specifying ‘soft’ causes GCC to generate output containing library calls for 
floating-point operations. ‘softfp’ allows the generation of code using hardware 
floating-point instructions, but still uses the soft-float calling conventions. 
‘hard’ allows generation of floating-point instructions and uses FPU-specific 
calling conventions.

    The default depends on the specific target configuration. Note that the 
hard-float and soft-float ABIs are not link-compatible; you must compile your 
entire program with the same ABI, and link with a compatible set of libraries.

* -mlittle-endian
    为了在小端模式下运行的处理器所生成的代码。这是所有标准配置的默认值。

    Generate code for a processor running in little-endian mode. This is the 
default for all standard configurations.

-mbig-endian
    Generate code for a processor running in big-endian mode; the default is to 
compile code for a little-endian processor.
-mwords-little-endian
    This option only applies when generating code for big-endian processors. 
Generate code for a little-endian word order but a big-endian byte order. That 
is, a byte order of the form ‘32107654’. Note: this option should only be used 
if you require compatibility with code for big-endian ARM processors generated 
by versions of the compiler prior to 2.8. This option is now deprecated.
-march=name
    This specifies the name of the target ARM architecture. GCC uses this name 
to determine what kind of instructions it can emit when generating assembly 
code. This option can be used in conjunction with or instead of the -mcpu= 
option. Permissible names are: ‘armv2’, ‘armv2a’, ‘armv3’, ‘armv3m’, ‘armv4’, 
‘armv4t’, ‘armv5’, ‘armv5t’, ‘armv5e’, ‘armv5te’, ‘armv6’, ‘armv6j’, ‘armv6t2’, 
‘armv6z’, ‘armv6zk’, ‘armv6-m’, ‘armv7’, ‘armv7-a’, ‘armv7-r’, ‘armv7-m’, 
‘armv7e-m’, ‘armv7ve’, ‘armv8-a’, ‘armv8-a+crc’, ‘iwmmxt’, ‘iwmmxt2’, ‘ep9312’.

    -march=armv7ve is the armv7-a architecture with virtualization extensions.

    -march=armv8-a+crc enables code generation for the ARMv8-A architecture 
together with the optional CRC32 extensions.

    -march=native causes the compiler to auto-detect the architecture of the 
build computer. At present, this feature is only supported on Linux, and not all 
architectures are recognized. If the auto-detect is unsuccessful the option has 
no effect.
-mtune=name
    This option specifies the name of the target ARM processor for which GCC 
should tune the performance of the code. For some ARM implementations better 
performance can be obtained by using this option. Permissible names are: ‘arm2’, 
‘arm250’, ‘arm3’, ‘arm6’, ‘arm60’, ‘arm600’, ‘arm610’, ‘arm620’, ‘arm7’, 
‘arm7m’, ‘arm7d’, ‘arm7dm’, ‘arm7di’, ‘arm7dmi’, ‘arm70’, ‘arm700’, ‘arm700i’, 
‘arm710’, ‘arm710c’, ‘arm7100’, ‘arm720’, ‘arm7500’, ‘arm7500fe’, ‘arm7tdmi’, 
‘arm7tdmi-s’, ‘arm710t’, ‘arm720t’, ‘arm740t’, ‘strongarm’, ‘strongarm110’, 
‘strongarm1100’, ‘strongarm1110’, ‘arm8’, ‘arm810’, ‘arm9’, ‘arm9e’, ‘arm920’, 
‘arm920t’, ‘arm922t’, ‘arm946e-s’, ‘arm966e-s’, ‘arm968e-s’, ‘arm926ej-s’, 
‘arm940t’, ‘arm9tdmi’, ‘arm10tdmi’, ‘arm1020t’, ‘arm1026ej-s’, ‘arm10e’, 
‘arm1020e’, ‘arm1022e’, ‘arm1136j-s’, ‘arm1136jf-s’, ‘mpcore’, ‘mpcorenovfp’, 
‘arm1156t2-s’, ‘arm1156t2f-s’, ‘arm1176jz-s’, ‘arm1176jzf-s’, ‘cortex-a5’, 
‘cortex-a7’, ‘cortex-a8’, ‘cortex-a9’, ‘cortex-a12’, ‘cortex-a15’, ‘cortex-a53’, 
‘cortex-a57’, ‘cortex-r4’, ‘cortex-r4f’, ‘cortex-r5’, ‘cortex-r7’, ‘cortex-m4’, 
‘cortex-m3’, ‘cortex-m1’, ‘cortex-m0’, ‘cortex-m0plus’, ‘marvell-pj4’, ‘xscale’, 
‘iwmmxt’, ‘iwmmxt2’, ‘ep9312’, ‘fa526’, ‘fa626’, ‘fa606te’, ‘fa626te’, ‘fmp626’, 
‘fa726te’.

    Additionally, this option can specify that GCC should tune the performance 
of the code for a big.LITTLE system. Permissible names are: 
‘cortex-a15.cortex-a7’, ‘cortex-a57.cortex-a53’.

    -mtune=generic-arch specifies that GCC should tune the performance for a 
blend of processors within architecture arch. The aim is to generate code that 
run well on the current most popular processors, balancing between optimizations 
that benefit some CPUs in the range, and avoiding performance pitfalls of other 
CPUs. The effects of this option may change in future GCC versions as CPU models 
come and go.

    -mtune=native causes the compiler to auto-detect the CPU of the build 
computer. At present, this feature is only supported on Linux, and not all 
architectures are recognized. If the auto-detect is unsuccessful the option has 
no effect.
-mcpu=name
    This specifies the name of the target ARM processor. GCC uses this name to 
derive the name of the target ARM architecture (as if specified by -march) and 
the ARM processor type for which to tune for performance (as if specified by 
-mtune). Where this option is used in conjunction with -march or -mtune, those 
options take precedence over the appropriate part of this option.

    Permissible names for this option are the same as those for -mtune.

    -mcpu=generic-arch is also permissible, and is equivalent to -march=arch 
-mtune=generic-arch. See -mtune for more information.

    -mcpu=native causes the compiler to auto-detect the CPU of the build 
computer. At present, this feature is only supported on Linux, and not all 
architectures are recognized. If the auto-detect is unsuccessful the option has 
no effect.
-mfpu=name
    This specifies what floating-point hardware (or hardware emulation) is 
available on the target. Permissible names are: ‘vfp’, ‘vfpv3’, ‘vfpv3-fp16’, 
‘vfpv3-d16’, ‘vfpv3-d16-fp16’, ‘vfpv3xd’, ‘vfpv3xd-fp16’, ‘neon’, ‘neon-fp16’, 
‘vfpv4’, ‘vfpv4-d16’, ‘fpv4-sp-d16’, ‘neon-vfpv4’, ‘fp-armv8’, ‘neon-fp-armv8’, 
and ‘crypto-neon-fp-armv8’.

    If -msoft-float is specified this specifies the format of floating-point 
values.

    If the selected floating-point hardware includes the NEON extension (e.g. 
-mfpu=‘neon’), note that floating-point operations are not generated by GCC's 
auto-vectorization pass unless -funsafe-math-optimizations is also specified. 
This is because NEON hardware does not fully implement the IEEE 754 standard for 
floating-point arithmetic (in particular denormal values are treated as zero), 
so the use of NEON instructions may lead to a loss of precision.
-mfp16-format=name
    Specify the format of the __fp16 half-precision floating-point type. 
Permissible names are ‘none’, ‘ieee’, and ‘alternative’; the default is ‘none’, 
in which case the __fp16 type is not defined. See Half-Precision, for more 
information.
-mstructure-size-boundary=n
    The sizes of all structures and unions are rounded up to a multiple of the 
number of bits set by this option. Permissible values are 8, 32 and 64. The 
default value varies for different toolchains. For the COFF targeted toolchain 
the default value is 8. A value of 64 is only allowed if the underlying ABI 
supports it.

    Specifying a larger number can produce faster, more efficient code, but can 
also increase the size of the program. Different values are potentially 
incompatible. Code compiled with one value cannot necessarily expect to work 
with code or libraries compiled with another value, if they exchange information 
using structures or unions.
-mabort-on-noreturn
    Generate a call to the function abort at the end of a noreturn function. It 
is executed if the function tries to return.
-mlong-calls
-mno-long-calls
    Tells the compiler to perform function calls by first loading the address of 
the function into a register and then performing a subroutine call on this 
register. This switch is needed if the target function lies outside of the 
64-megabyte addressing range of the offset-based version of subroutine call 
instruction.

    Even if this switch is enabled, not all function calls are turned into long 
calls. The heuristic is that static functions, functions that have the 
‘short-call’ attribute, functions that are inside the scope of a ‘#pragma 
no_long_calls’ directive, and functions whose definitions have already been 
compiled within the current compilation unit are not turned into long calls. The 
exceptions to this rule are that weak function definitions, functions with the 
‘long-call’ attribute or the ‘section’ attribute, and functions that are within 
the scope of a ‘#pragma long_calls’ directive are always turned into long calls.

    This feature is not enabled by default. Specifying -mno-long-calls restores 
the default behavior, as does placing the function calls within the scope of a 
‘#pragma long_calls_off’ directive. Note these switches have no effect on how 
the compiler generates code to handle function calls via function pointers.
-msingle-pic-base
    Treat the register used for PIC addressing as read-only, rather than loading 
it in the prologue for each function. The runtime system is responsible for 
initializing this register with an appropriate value before execution begins.
-mpic-register=reg
    Specify the register to be used for PIC addressing. For standard PIC base 
case, the default will be any suitable register determined by compiler. For 
single PIC base case, the default is ‘R9’ if target is EABI based or 
stack-checking is enabled, otherwise the default is ‘R10’.
-mpic-data-is-text-relative
    Assume that each data segments are relative to text segment at load time. 
Therefore, it permits addressing data using PC-relative operations. This option 
is on by default for targets other than VxWorks RTP.
-mpoke-function-name
    Write the name of each function into the text section, directly preceding 
the function prologue. The generated code is similar to this:

                   t0
                       .ascii "arm_poke_function_name", 0
                       .align
                   t1
                       .word 0xff000000 + (t1 - t0)
                   arm_poke_function_name
                       mov     ip, sp
                       stmfd   sp!, {fp, ip, lr, pc}
                       sub     fp, ip, #4

    When performing a stack backtrace, code can inspect the value of pc stored 
at fp + 0. If the trace function then looks at location pc - 12 and the top 8 
bits are set, then we know that there is a function name embedded immediately 
preceding this location and has length ((pc[-3]) & 0xff000000).
-mthumb
-marm
    Select between generating code that executes in ARM and Thumb states. The 
default for most configurations is to generate code that executes in ARM state, 
but the default can be changed by configuring GCC with the --with-mode=state 
configure option.
-mtpcs-frame
    Generate a stack frame that is compliant with the Thumb Procedure Call 
Standard for all non-leaf functions. (A leaf function is one that does not call 
any other functions.) The default is -mno-tpcs-frame.
-mtpcs-leaf-frame
    Generate a stack frame that is compliant with the Thumb Procedure Call 
Standard for all leaf functions. (A leaf function is one that does not call any 
other functions.) The default is -mno-apcs-leaf-frame.
-mcallee-super-interworking
    Gives all externally visible functions in the file being compiled an ARM 
instruction set header which switches to Thumb mode before executing the rest of 
the function. This allows these functions to be called from non-interworking 
code. This option is not valid in AAPCS configurations because interworking is 
enabled by default.
-mcaller-super-interworking
    Allows calls via function pointers (including virtual functions) to execute 
correctly regardless of whether the target code has been compiled for 
interworking or not. There is a small overhead in the cost of executing a 
function pointer if this option is enabled. This option is not valid in AAPCS 
configurations because interworking is enabled by default.
-mtp=name
    Specify the access model for the thread local storage pointer. The valid 
models are soft, which generates calls to __aeabi_read_tp, cp15, which fetches 
the thread pointer from cp15 directly (supported in the arm6k architecture), and 
auto, which uses the best available method for the selected processor. The 
default setting is auto.
-mtls-dialect=dialect
    Specify the dialect to use for accessing thread local storage. Two dialects 
are supported—‘gnu’ and ‘gnu2’. The ‘gnu’ dialect selects the original GNU 
scheme for supporting local and global dynamic TLS models. The ‘gnu2’ dialect 
selects the GNU descriptor scheme, which provides better performance for shared 
libraries. The GNU descriptor scheme is compatible with the original scheme, but 
does require new assembler, linker and library support. Initial and local exec 
TLS models are unaffected by this option and always use the original scheme.
-mword-relocations
    Only generate absolute relocations on word-sized values (i.e. R_ARM_ABS32). 
This is enabled by default on targets (uClinux, SymbianOS) where the runtime 
loader imposes this restriction, and when -fpic or -fPIC is specified.
-mfix-cortex-m3-ldrd
    Some Cortex-M3 cores can cause data corruption when ldrd instructions with 
overlapping destination and base registers are used. This option avoids 
generating these instructions. This option is enabled by default when 
-mcpu=cortex-m3 is specified.
-munaligned-access
-mno-unaligned-access
    Enables (or disables) reading and writing of 16- and 32- bit values from 
addresses that are not 16- or 32- bit aligned. By default unaligned access is 
disabled for all pre-ARMv6 and all ARMv6-M architectures, and enabled for all 
other architectures. If unaligned access is not enabled then words in packed 
data structures will be accessed a byte at a time.

    The ARM attribute Tag_CPU_unaligned_access will be set in the generated 
object file to either true or false, depending upon the setting of this option. 
If unaligned access is enabled then the preprocessor symbol 
__ARM_FEATURE_UNALIGNED will also be defined.
-mneon-for-64bits
    Enables using Neon to handle scalar 64-bits operations. This is disabled by 
default since the cost of moving data from core registers to Neon is high.
-mslow-flash-data
    Assume loading data from flash is slower than fetching instruction. 
Therefore literal load is minimized for better performance. This option is only 
supported when compiling for ARMv7 M-profile and off by default.
-mrestrict-it
    Restricts generation of IT blocks to conform to the rules of ARMv8. IT 
blocks can only contain a single 16-bit instruction from a select set of 
instructions. This option is on by default for ARMv8 Thumb mode. 
