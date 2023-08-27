# FreeRTOS SMP Template for Raspberry Pi Pico Board

* [Introduction to Symmetric Multiprocessing (SMP) with FreeRTOS](./SMP.md)
* [Port from FreeRTOS non-SMP version to FreeRTOS SMP version](./Porting-to-FreeRTOS-SMP-Kernel.md)

## Building and Running the RTOS Template Applications

### Building
To compile this project firstly initialize and update the submodules: 
```
 git submodule update --init
```
1. Setup the Raspberry Pi Pico SDK build environment by following the instructions for
[Getting Started With Pico](https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf).
Ensure that `PICO_SDK_PATH` is set in your environment, or pass it via
`-DPICO_SDK_PATH=xxx` on the CMake command line.
2. Run the following commands:
```sh
$ mkdir build
$ cd build
$ cmake ..
$ make
```
This will generate `.uf2` files for each Template application: `build/pico-freertos.uf2`

### Running
1. Connect the Raspberry Pi Pico to your computer while holding the `BOOTSEL`
button. This will force the board into USB Mass Storage Mode.
2. Drag-and-drop the `.uf2` file for the template you want to run onto the Mass
Storage Device.
----

## RTOS Configuration and Usage Details
* Configuration items specific to the template are contained in
`include/FreeRTOSConfig.h`.
* The [constants defined in these files](https://www.freertos.org/a00110.html) can be
edited to suit your application.
* The following configuration options are specific to the SMP support in the FreeRTOS Kernel:
  * `configNUM_CORES` - Set the number of cores.
  * `configRUN_MULTIPLE_PRIORITIES` - Enable/Disable simultaneously running tasks with multiple priorities.
  * `configUSE_CORE_AFFINITY` - Enable/Disable setting a task's affinity to certain cores.
  * `Source/Portable/MemMang/heap_4.c` is included in the project to provide the
memory allocation required by the RTOS kernel. Please refer to the
[Memory Management](https://www.freertos.org/a00111.html) section of the API
documentation for complete information.
* vPortEndScheduler() has not been implemented.