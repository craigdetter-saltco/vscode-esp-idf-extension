# ESP-IDF Extension features for Visual Studio Code

This extension provides many features to ease development of ESP-IDF Projects.

- Quick [Configure ESP-IDF extension](./SETUP.md) for first time user to help the user download, install and setup ESP-IDF and required tools within this Visual Studio Code extension.
- Quick prototyping by copying ESP-IDF examples with **ESP-IDF: Show ESP-IDF Examples Projects**.
- Syntax highlighting for [KConfig](#Kconfig-files-editor) and ESP-IDF Kconfig style syntax validation if `idf.useIDFKconfigStyle` is enabled.
- GUI [SDK Configuration editor](#SDK-Configuration-editor) to configure your ESP-IDF project (esp-idf menuconfig).
- [Partition table editor](./PARTITION_TABLE_EDITOR.md)
- [NVS Partition editor](./NVS_PARTITION_EDITOR.md)
- Easily [Build](#Build), [Flash](#Flash) and [Monitor](#Monitor) your code for ESP32 and ESP32 S2 chips.
- OpenOCD server within Visual Studio Code.
- [DEBUGGING](./DEBUGGING.md) with [ESP-IDF Debug Adapter](https://github.com/espressif/esp-debug-adapter).
- Size analysis of binaries with **ESP-IDF: Size analysis of the binaries**.
- App tracing when using ESP-IDF Application Level Tracing Library like in [ESP-IDF Application Level Tracing Example](https://github.com/espressif/esp-idf/tree/master/examples/system/app_trace_to_host).
- [Heap tracing](./HEAP_TRACING.md)
- [System view tracing viewer](./SYS_VIEW_TRACING_VIEWER.md)
- Localization (English, Chinese, Spanish) of commands which you can also [add a language contribution](./LANG_CONTRIBUTE.md).
- [Code Coverage](./COVERAGE.md) for editor source highlighting and generate HTML reports.
- Search text editor's selected text in ESP-IDF documentation with **ESP-IDF: Search in documentation...** right click command or with its [keyboard shortcut](#Available-commands). Results will be shown in ESP-IDF Explorer Tab if found on ESP-IDF Documentation based on your current vscode language, ESP-IDF version in `idf.espIdfPath` (latest otherwise) and `idf.adapterTargetName`.
- [ESP Rainmaker support](./ESP_RAINMAKER.md)
- [Core dump and GdbStub](./POSTMORTEM.md) postmortem mode.
- [CMake Editor](#CMake-Editor)
- [Support for WSL 2](./WSL.md)

## Arduino as ESP-IDF component

The **Add Arduino-ESP32 as ESP-IDF Component** command will add [Arduino-ESP32](https://github.com/espressif/arduino-esp32) as a ESP-IDF component in your current directory (`${CURRENT_DIRECTORY}/components/arduino`). You can also use the **Create ESP-IDF project** command with `arduino-as-component` template to create a new project directory that includes Arduino-esp32 as an ESP-IDF component.

> **NOTE** Not all versions of ESP-IDF are supported. Make sure to check [Arduino-ESP32](https://github.com/espressif/arduino-esp32) to see if your ESP-IDF version is compatible.

## Build

**ESP-IDF: Build your project** is provided by this extension to build your project using `CMake` and `Ninja-build` as explained in [ESP-IDF Build system using Cmake directly](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#using-cmake-directly).

## Debugging

Click <kbd>F5</kbd> to start debugging. To configure the debug behaviour, please review [DEBUGGING](./DEBUGGING.md).

> **NOTE** For correct debug experience, first `build` your project, choose the right serial port, `flash` your device and define the correct `idf.customExtraPaths` paths and `idf.customExtraVars` using [SETUP](./SETUP.md).

## CMakeLists.txt Editor

**THIS WILL OVERRIDE ANY EXISTING CODE IN THE FILE WITH THE ONE GENERATED IN THE EDITOR. IF YOU HAVE ANY CODE NOT INCLUDED IN THE [SCHEMA](../cmakeListsSchema.json) (OR SINGLE LINE COMMENTS) USE A REGULAR TEXT EDITOR INSTEAD**

On CMakeLists.txt file right click this extension provides a custom CMakeLists.txt Editor to fill an ESP-IDF Project and Component registration as specified in [ESP-IDF Project CMakeLists.txt](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#project-cmakelists-file) and [ESP-IDF Component CMakeLists.txt files](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#component-cmakelists-files). You need to choose which kind of CMakeLists.txt file (project or component) to edit. There is 2 types of input, one is a simple string and another is an array of strings, such as Component Sources (SRCS). All inputs are described in the CMakeLists.txt Schema (\${this_repository}/src/cmake/cmakeListsSchema.json).

> **NOTE** This editor doesn't support all CMake functions and syntaxes. This editor should only be used for simple CMakeLists.txt options such as component registration (using idf_component_register) and basic project elements. If you need more customization or advanced CMakeLists.txt, consider reviewing [ESP-IDF Build System](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html). Also review [CMakeLists.txt editor schema](../cmakeListsSchema.json) for a list of supported code.

## Flash

**ESP-IDF: Flash your project** is provided by this extension to flash your project using the ESP-IDF `esptool.py` as explained in [ESP-IDF Build system Flash arguments](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html#flash-arguments). This command depends on the `${YOUR_PROJECT_DIR}/build/flasher_args.json` file generated by [build](#Build) and the `idf.flashBaudRate` configuration setting.

## Kconfig files editor

When you open a `Kconfig`, `Kconfig.projbuild` or `Kconfig.in` file we provide syntax highlighting. If `idf.useIDFKconfigStyle` is enabled, we also provide ESP-IDF Kconfig style syntax validation such as indent validation and not closing blocks found (Example: menu-endmenu). Please review [Kconfig Formatting Rules](https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/kconfig.html) and [Kconfig Language](https://github.com/espressif/esp-idf/blob/master/tools/kconfig/kconfig-language.txt) for further details about the ESP-IDF Kconfig formatting rules and Kconfig language in general.

## Log & Heap Tracing

We support [log](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/app_trace.html) and [heap tracing](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/system/heap_debug.html) out of the box, which enables users to perform log/heap tracing with just few button clicks and present the results of tracing data with UI.

You can follow [this](./HEAP_TRACING.md) quick step-by-step guide for heap tracing.

## Monitor

**ESP-IDF: Monitor your device** is provided by this extension to start `idf.py monitor` terminal program in Visual Studio Code. Please take a look at the [IDF Monitor documentation](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-monitor.html?highlight=monitor).

## SDK Configuration editor

### Prerequisites

- ESP-IDF `>=v4.x`

This plugin includes a GUI menuconfig that reads your current project folder's sdkconfig file (if available, otherwise it would take default values) and start the [ESP-IDF JSON configuration server](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html?highlight=confserver#json-configuration-server) process (confserver.py in **\${ESP-IDF-DIRECTORYPATH}**/tools) that enables the user to redefine ESP-IDF project and board configuration.

When the user modify a parameter value, the value is send to the `confserver.py` process, which return the new value and other values modified to GUI menuconfig and then update the values in the UI.

Values are not automatically saved to the sdkconfig file until you click save changes. You can cancel any changes and load the values from the sdkconfig file by clicking cancel changes. If you click set default the current sdkconfig file is replaced by a template sdkconfig file and then loaded into the GUI menuconfig rendered values.

The search functionality allows to find a parameter by description, i.e the name that appears in the sdkconfig file.

An IDF GUI Menuconfig log in Output (Menu View -> Output) is created to print all communications with `${idf.espIdfPath}\tools\confserver.py`. It can be be used to track any errors.

## Set Espressif device target

The **ESP-IDF: Set Espressif device target** allows the user to choose among Espressif different chips based on [idf.py set-target](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/build-system.html?highlight=target#selecting-idf-target).

## System View Tracing Viewer

We have provide a [system view tracing viewer](./SYS_VIEW_TRACING_VIEWER.md) inside the vscode extension which will enable you to view the traces along with other relevant details.