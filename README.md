# Welcome to the `Book Club Code` site!

This is a place for the Embedded.fm book club to collaborate and learn together.

## Repo Structure Guide

### Top-level folders currently include:
* **[Books](https://github.com/cadet702/Embedded-STM32/tree/main/Books)** - For code directly related to chapters and exercises in the books we read.
* **[Playground](https://github.com/cadet702/Embedded-STM32/tree/main/Playground)** - For individuals to create their own subfolders for whatever they want.
* **[Tools](https://github.com/cadet702/Embedded-STM32/tree/main/Tools)** - For sharing and iterating on general purpose code, drivers, and tools.


## Contributing to Book Club Code

There are two main options for contributing to this repo: issues and pull requests.

### Issues

A GitHub **[Issue](https://github.com/cadet702/Embedded-STM32/issues)** is a ticket you create that logs a specific problem, a bug, a feature request, or an inquiry. This issue will be logged centrally and responded to by other people in this community.

> _**Issues are ideal when you see something which can be improved but there isn't an obvious fix.**_

### Pull Requests

A GitHub **[Pull Request](https://github.com/cadet702/Embedded-STM32/pulls)** ("PR") is a request for the site maintainers to _pull in_ changes that have been authored by other users.

> _**PRs are ideal when you already know how to improve the site and want to propose a set of specific changes.**_


## Other Important Links

* [Into to GIT](https://levelup.gitconnected.com/git-doesnt-have-to-be-hard-e1e115be6668) - A great article helping GIT make slightly more sense.
* [Embedded.fm](https://embedded.fm/) - Description needed...
* [Keil](https://keil.com) - Place to get a variety of compilers.
* [IAR](https://IAR.com) - Place to get the IAR compiler.

## Guides and Documentation

* **TBD** - Guides to be added here:
  * Windows TBD
  * Mac TBD
  * Linux TBD
* Compiling STM32 applications using gcc and make (Nathan Jones)
  1) Download and install [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) (don't worry; no one is going to make you use the HAL!).
  2) Once finished, open STM32CubeMX and create a new project for your specific processor.
  3) Click the "Project Manager" tab and change "Toolchain/IDE" to "Makefile".
  4) Change any other desired settings in CubeMX, save the project, and then click "Generate Code".
    - CubeMX will automatically generate code to initialize the clock based on the settings in the "Clock Configuration" tab. If you'd rather set up the clock yourself, delete the call to `SystemClock_Config()` in your main file.
    - The SWD pins, used for debugging and programming, are **disabled** by default. I'd recommend at least enabling them so you can debug your STM32 and so you won't have to erase your STM32 device every time you want to reflash it with a debug adapter. To do that, click the "Pinout & Configuration" tab. Under "Categories", expand "System Core" and select "SYS". In the toolbar that opens up, change "Debug" to "Serial Wire".
  5) In your generated project, open up "Core/Src/main.c" and write your application!
    - You can find register definitions for the STM32 in "Drivers/CMSIS/Device/ST/STM32XXXX/Include". Register definitions for the Arm core are in "Drivers/CMSIS/Core/Include".
    - If you're slavishly opposed to using *any* of the pre-written start-up code you'll still need to generate a project using CubeMX since I don't know of any quicker way to get the linker script. Once you've created your project, delete the contents of "Core/Src/main.c" and write your application (don't forget to add the appropriate header files!). When you go to build your project, you'll need the files below. You'll also need to include ("-I") most of the folders listed in the makefile, such as "Core/Inc", "Drivers/CMSIS/Device/ST/STM32F3xx/Include", and "Drivers/CMSIS/Include".
      - Core/Src/main.c
      - Core/Src/system_stm32XXXX.c
      - startup_stm32XXXX.S
      - STM32XXX_FLASH.ld
    - Note: Some of the STM32 HAL will still be compiled with your application (for instance, the HAL tick, which lets you use `HAL_Delay()`). To remove this from your binary I think you'll either have to root it out by hand (i.e. follow the initialization code to find which parts start up the HAL tick and other functions and remove those function calls) or start from scratch, by deleting everything in `main.c`, as was mentioned above.
  6) Compile your project by executing `make` from a terminal window opened to your project folder.
  7) Upload your project using your method of choice.
* Other guides
