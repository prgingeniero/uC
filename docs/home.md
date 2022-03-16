

# Deploying TinyML

https://learning.edx.org/course/course-v1:HarvardX+TinyML3+1T2021/home


## C++ for Python Users

C++ for Python Users

If you are comfortable with C/C++, please feel free to move on to the next reading. If you are new to C++, we hope this introductory material will be helpful for you. If you are comfortable with C/C++, please feel free to move on to the next reading. If you are new to C++, we hope this introductory material will be helpful for you.

Python, the language you have been using in all of your Colabs, is a dynamically-typed, “high-level” language that is interpreted at runtime. C++ (also written as Cpp), on the other hand, is a statically-typed, “low-level” language that is pre-compiled before running, allowing for very compact code. 

The good news is that since we are using the Arduino platform, we won’t have to deal with much of the complications of C++ as that is taken care of for us by the many libraries and board files we will be able to leverage (more on that soon). We’ll then just have to pay attention to the changes in syntax which are more cosmetic than functional. That is, all of the main loops and conditional statements (e.g., for, if-else) remain the same functionally!

In order to make sure you feel comfortable we’ve put together a set of short appendix items and have collected some other good resources to walk you through the main changes between Python and C++ for Arudino which you can find below. As you go through the course, if you have good ideas for other introductory material, changes to the current material, or additional resources, please let us know and we’d be very excited to add them to the list for future learners!

For more information, take a look at our short appendix document that covers:

            Data Types
            Scope, Parentheses, and Semicolons
            Functions
            Libraries, Header Files, #include
            Other General Syntax Points

Additional resources:

            The C++ Language Tutor
            The Google C++ Style Guide
            The Arduino Standard Library Language Reference

## Diversity of Embedded Systems

Embedded Systems

In this reading, we will explore the diversity of embedded systems.

If you take a few minutes to look around the room you’re in, you’ll no doubt recognize the proliferation of embedded hardware within our world. Embedded systems are increasingly ubiquitous because they serve to complete specific computational tasks within their environment, allowing us to not only collect all sorts of data from distributed sensors but also to process the resulting information locally and act accordingly. That we can accomplish this in situ, or within the environment that this hardware is embedded within, at a fraction of the cost and physical scale of most general-purpose computing hardware, opens the door to many advancements in automation and generally to the creation of smart, connected things.

While the specifications and capabilities of a given embedded system ought to be tailored for its application, in general, we can look to the common construct for an embedded system that links sensing to processing and later actuation through the process of transduction, the conversion of one form of energy into another, for throughlines. In sense, we convert energy from a physical phenomenon into an electrical signal we can go on to digitize and compute with. In actuation, the converse. In this course, we’ll focus predominantly on the central element of said construct: the computing hardware, and review specifications and technical considerations that vary between implementations of embedded systems.

An image of the Arduino Nano 33 BLE Sense noting the location of the IMU, USB port, Microphone, temperature + humidity sensors, and processor + bluetooth module.

Development Boards

In the context of this course, we have talked about and deployed a microcontroller unit (or MCU) development board from Arduino, the Nano 33 BLE Sense. Here, we distinguish the nRF52840 MCU from the development board it is soldered to. What’s interesting about this board is that despite its relatively small size, it is jam-packed with many of the representative elements of an embedded system, all on one printed circuit board (PCB): a collection of surface-mount sensors, a form of an actuator in the on-board programmable RGB LED, and an integrated MCU-BLE module, where BLE is an acronym for a branch of the Bluetooth standard called Bluetooth Low Energy. Further still, the PCB that the MCU is soldered to serves to ‘break out’ additional IO from the controller to provide interfaces for external, off-board modules and connections to daughter boards. So, while in many ways, the Nano 33 BLE Sense is representative of an embedded system, it is separated from commercial implementations in that it serves no particular purpose, other than the open-ended development of an application that is. Put another way, a development board has the advantage of enabling many potential use cases. Further, you don’t have to go through the process of designing circuitry, capturing schematics, or physical layout for such a board to get started prototyping a concept that could go on to be manufactured with specific intent later. The tradeoffs you make in employing a development board often involve board size and cost.

Board Size

Board size, and shape, have fairly meaningful implications for use in the field, given these simple parameters constrain where and how a system can be deployed. Some environments or contexts within which we’d like to embed a system are forgiving (like the Google Home, say), but other manifestations (smart glasses, for example) depend wholly on the requisite hardware being quite tiny and perhaps of unique form. Somewhat obviously, board size is determined by the number and physical size, or package, of the components that live upon it. At a minimum, an embedded system must include a MCU chip alongside a power source, often a lithium polymer battery, and power circuitry. The nRF52840 MCU on the Nano 33 BLE Sense lives within a MCU-BLE module, the U-Blox NINA-B306, which spans 10 by 15 mm, dimensions that include a trace antenna. The MPM3610 step-down converter used to down-regulate the 5V delivered to the board over USB occupies 3 by 5 mm, alongside small SMD passives. The entire board, meanwhile, spans 18 by 45 mm. While impressive, clearly a purpose-designed PCB could remove some of the sensors and IO breakout unnecessary for a specific application to reduce the overall scale even further, perhaps by about 60 to 70%.

Cost

Unsurprisingly, the cost of a development board scales with its MCU’s compute capability and general feature set. In selecting the appropriate MCU for an application, it is important to remember that MCUs are often deployed to complete specific tasks, where the complexity they will face is predetermined or constrained. For very simple tasks, we highlight the ATTINY85 (an 8-bit processor with 8 kB of flash) that can, depending on the package selected, cost well less than $1 EA and even less at scale, perfect for simple computing requirements. In the context of TinyML, the AI-capable NINA-B306 module featuring the Nordic Semiconductor nRF52840 chip (an ARM Cortex M4) and all-in-one BLE hardware (including antenna) costs about $10 EA and is more generally representative. In view of the on-board sensors and design costs, the Arduino Nano 33 BLE Sense costs just over $30, not even an hour's time of an electrical engineer who might design such a board — a tremendous value. In general, the boards we originally considered for this class span from $2 (BluePill) to $54 (Disco-F746NG).

You can find a list of the boards we considered in the table below. Ultimately, our staff selected the Arduino Nano 33 BLE Sense for its versatility, in providing a large selection of on-board sensors, accessible IO via breakout pins, and a BLE module for projects that involve wireless communication, with reasonably representative compute specifications for resource-constrained hardware. We’ll explore the compute specifications in a bit more detail in the next video and reading.

TinyML Development Board Comparison                    ◽officially TFLM supported   ▢ unofficially compatible boards
Board	MCU	CPU	Clock	Memory	IO	Sensor(s)	Radio
Arduino Nano 33 BLE Sense 	Nordic nRF52840 	32-bit ARM Cortex-M4F 	64 MHz 	1 MB flash 256 kB RAM 	x8 12-bit ADCs x14 DIO UART, I2C, SPI 	Mic, IMU, temp, humidity, gesture, pressure, proximity, brightness, color 	BLE
Espressif ESP32-DevKitC 	ESP32 D0WDQ6 	32-bit, 2-core Xtensa LX6 	240 MHz 	4 MB flash 520 kB RAM 	x18 12-bit ADCs x34 DIO** UART, I2C, SPI 	Hall effect, capacitive touch*** 	WiFi, BLE
Espressif EYE 	ESP32 D0WD 	32-bit, 2-core Xtensa LX6 	240 MHz 	4 MB flash* 520 kB RAM 	SPI via surface pads 	Mic, camera 	WiFi, BLE
Teensy 4.0 	NXP iMXRT1062 	32-bit ARM Cortex-M7 	600 MHz 	2 MB flash 1 MB RAM 	x14 10-bit ADCs x40 DIO** UART, I2C, SPI 	Internal temperature, capacitive touch 	None
MAX32630FTHR 	Maxim MAX32620 	32-bit ARM Cortex-M4F 	96 MHz 	2 MB flash 512 kB RAM 	x4 10-bit ADCs x16 DIO UART, I2C, SPI 	Accelerometer, gyroscope 	BLE

*This board also features 4 MB flash and 8 MB of PSRAM external to the MCU, **shared programmable functions, ***with external touchpads 
Board	ASIC	DSP	Clock	Memory	IO	Sensor(s)	Radio
Himax WiseEye WE-I Plus EVB 	HX6537-A 	32-bit ARC EM9D DSP 	400 MHz 	2 MB flash 2 MB RAM 	x3 DIO I2C 	Mic, accelerometer, camera 	None

We include the Himax WiseEye as an officially supported example of hardware optimization for TensorFlow Lite that calls on an application-specific integrated circuit (ASIC).


## Arduino Cores, Frameworks, mbedOS, and ‘Bare Metal’


Arduino Cores, Frameworks, mbedOS, and ‘Bare Metal’

In working with the Nano 33 BLE Sense, you have interacted with some of the underlying layers between your application and the board’s physical hardware. Here, we quickly define some key terms (Arduino core, embedded frameworks, mbedOS, RTOS, and bare-metal) before discussing the implications of these concepts to your application.

What is an Arduino Core?

An Arduino “core” is central to a particular microcontroller’s compatibility with the Arduino framework. You can think of it as a low-level software API for a specific chip or family, like AVR or SAMD. Since each microcontroller has its own architecture, the concomitant core acts as an abstraction layer between your application and the physical hardware. In this context, libraries can be thought of as extensions to the core that are portable between chips or board variants for a particular chip.

More granularly, each Arduino core contains a pair of generic files: arduino.h that handles declarations for what are often called ‘built-in’ functions like pinMode(), digitalWrite(), analogRead(), delay(), et cetera as well as macros for constants, like HIGH or INPUT_PULLUP, and operations like bitToggle() or abs(); main.cpp declares the basic program structure for a sketch, as it relates to setup() and loop(). We should note that arduino.h also sets the stage for board-specific pin mappings defined in pins_arduino.h at <architecture>/variants/<board name>. 

The remainder of a core is largely architecture-specific. There is a collection of C files with names wiring.c and wiring_<type>.c that define hardware initialization, timing, and functions related to IO of various types, like analogRead(). This nomenclature is a nod to the Wiring API that Arduino utilizes. There are also the header and C++ files for serial classes Stream, Print, and HardwareSerial, alongside a light USB stack. If you’re interested in digging deeper into a specific core, check out this appendix document.

What is an Embedded Framework?

Loosely, to account for variation between manifestations, an embedded framework is a collection of development tools for microcontrollers that may or may not be portable and often serve as some combination of low-level API, software development kit (SDK), and hardware abstraction layer (HAL). For instance, the Arduino framework comprises its integrated development environment (IDE), built-in functions (defined by cores), as well as library extensions. As an open-source project, the Arduino framework is perhaps a bit more difficult to put bounds around, given its reliance on related projects, namely Wiring and its predecessor Processing, born out of the MIT Media Lab. Here are some other examples:

CMSIS - Arm Cortex Microcontroller Software Interface Standard

FreeRTOS - a real-time operating system (RTOS) kernel for embedded devices

Mbed - an embedded RTOS for Internet-of-Things, drivers for I/O devices

STM32Cube - HAL between STM32 devices and other libraries

If you work with more than one framework, we recommend PlatformIO, an extension of Visual Studio Code, that enables you to call on many frameworks, with a unified workflow.

What is an RTOS?

Okay, so two of the examples we provide for embedded frameworks make mention of a real-time operating system or RTOS. In a circular definition, an RTOS is an operating system that serves real-time applications. More helpfully, an embedded RTOS is extremely light-weight system software that organizes the attention of microcontroller processing cores, often singular, to minimize unnecessary task switching and to prioritize time-sensitive computation so that the processing time required for a given task is ideally less than the interval to the next input. We won’t dwell on the details here, but you can learn more about task scheduling, apparent multitasking (threads), and other RTOS fundamentals, here.

What are Mbed and mbedOS?

Mbed is a competing embedded framework to Arduino, with a fair bit of overlap. A glance at the ‘What is Mbed?’ section of their landing page illustrates this. Both are centered around a C++ API and feature IDEs, example code, libraries, and drivers for common components. Perhaps most striking is the difference in accessibility and other professional-grade considerations Mbed makes, like security. Notably, while mbedOS can be and usually is an RTOS, for applications that require thread management, there is also a limited ‘bare metal’ profile that you can utilize to cut down on the memory utilization tied to RTOS overhead.

Why are we talking about mbedOS? Well, the Nano 33 BLE Sense runs on it. Here is an Arduino blog post from Martino Facchin, the head of Arduino’s firmware development team, that explains the Nano 33 BLE Sense unique core, and its reliance on mbedOS.

What is Bare Metal?

You may happen upon variations of this definition, but at a high, inclusive level, ‘bare metal’ programming in an embedded systems context means utilizing microcontroller hardware independent of an operating system or scheduler, at the least. Typically, there is a base super loop, not unlike the Arduino sketch structure, and all processing is defined by your application. In many cases, this also means your code is written independently of pre-existing frameworks. This is where you’ll find some variation in definitions. The colloquial spirit of bare-metal programming is counter to most developer mindsets, in that because microcontroller tasks are often simple but mission-critical, their developers want strict control over processing that precludes reliance on abstraction.

A ‘true’ bare-metal project, then, will have a developer that either writes or, if supplemented by a light-weight framework, fully understands each layer, from the physical hardware on up, using an MCU/SoC datasheet as their guide to registering definitions and hardware architecture.

Implications for your Application

As you can imagine, your choice of the framework (or lack thereof) should stem from the needs of your application. If you have no hard time-constraints, an RTOS could be eating away at precious resources that may be constrained. However, there are obvious challenges to developing a bare-metal solution, which can largely be summarized by ‘recreating known solutions.’ If your task is simple, time-insensitive, mission-critical, or needs to be deployed on very constrained hardware, a bare-metal approach may be appropriate, assuming you have the knowledge and time required for the development. If you have a complex web of tasks in front of you that could be organized by a scheduler, an RTOS is really a no-brainer. In most cases, there is room for innovation in the middle, where you place trust in proven frameworks and libraries, but manage processing attention in a simple base loop, perhaps organized as a finite state machine or FSM.






## What is TensorFlow Lite for Microcontrollers?


What is TF Lite Micro?

As a future TinyML engineer, it is essential to understand the inner workings of the software you use to know its capabilities and limitations. So, in the upcoming series of videos and readings, you will learn more about the challenges that led to the development of TF Lite Micro, straight from the source. Pete Warden from Google, who leads the team that works on TF Lite Micro, will introduce TF Lite Micro and give us a sneak peek into its internal workings. Here is a preview of what is to come next.

TensorFlow has become the most popular deep learning framework, superseding other popular frameworks such as PyTorch and Keras. TensorFlow, developed by Google, contains a Python frontend with highly optimized C++ code at its core, making it simple to program, fast, and efficient. The library has a large developer community and is now seen as the de facto standard for most machine learning applications.

Despite this, TensorFlow is not suitable for every scenario. The standard TensorFlow library is ~400 MB in size, and even running a relatively small model (e.g., 200 MB) can take up a considerable amount of random access memory (> 1 GB). Such large storage and memory requirements make running simple models on lightweight systems largely intractable.

Recognizing this issue, Google developed a more lightweight framework, TensorFlow Lite, also sometimes referred to as TensorFlow Mobile. The TFLite binary is approximately 1 MB in size, considerably more compact than the original library, making it possible to run deep learning models on mobile devices such as smartphones. This compression was achieved by removing superfluous functionality that is largely unnecessary for mobile deployment. 

While this is an improvement, our problem still remains: even TFLite is not suitable for every scenario. Many important deep learning applications exist at the microcontroller-level, which are significantly more resource-constrained than mobile devices, often equipped with less than 1 MB of storage and 256 KB RAM. Clearly, deploying TFLite models is not feasible for microcontrollers, so an alternative solution was needed.

Enter TF Lite Micro. TF Lite Micro takes the compression of the TensorFlow library to the extreme, removing all but essential functionality. In fact, the core runtime of the library takes up only 16 KB, several orders of magnitude smaller than TFLite. With such a small memory footprint, this lightweight framework makes it possible to deploy deep learning models on the smallest of microcontrollers, such as an Arduino Nano.

However,  this is not without its complications.  Deploying models with TF Lite Micro is fraught with new and unique challenges when building models. For example, since all functionality for plotting and debugging is removed, troubleshooting model issues is difficult. Additionally, since many microcontrollers do not have floating-point units or use 8-bit arithmetic, the model weights and activations must be suitably quantized on the microcontroller system. Since model training requires near-machine precision to perform gradient descent, this largely precludes on-device training. Thus, TF Lite Micro models must first be trained on a device with greater computational resources before being ported to the microcontroller, adding an additional stage to the machine learning workflow. 

Despite this, the benefits provided by TF Lite Micro - the ability to perform machine learning inference on microcontroller devices - far exceed the challenges, heralding a new era of machine learning that is often referred to as tiny machine learning.


## TensorFlow Lite Flatbuffer Manipulation Example

In this Colab, we’ll dig a little deeper into the TensorFlow Lite Flatbuffer file format. We’ll load in the Flatbuffer library and the TensorFlow Lite Schema, which will allow us to access and directly modify the weights in the pretrained KWS model manually. You’ll then get to see how your direct modifications impact the final model accuracy using the Speech Commands dataset!

https://colab.research.google.com/github/tinyMLx/colabs/blob/master/4-4-8-Flatbuffers.ipynb


## Summary of TFLM



TFLite Micro Developer Design Principles

There are four overarching design principles that TFMicro was built upon in order to address some of the challenges faced by developers when working with tinyML for embedded systems. This reading provides a synopsis of these core principles, as outlined in further detail in the TensorFlow Lite Micro paper.

Principle 1: Minimize Feature Scope for Portability

This principle proposes that an embedded machine learning (ML) framework should assume, by default, that the model, input data, and output arrays are in memory, and do not need to be loaded into memory. In addition, accessing peripherals, such as an on-device camera, should not be the job of the ML framework. These functions still need to be fulfilled, but principally should not be fulfilled by the ML framework.

While this may seem unimportant, some microcontrollers do not have memory management (e.g. malloc) and other capabilities. Thus, trying to accommodate all varieties of platforms would bloat the library in an attempt to provide sufficient portability. Fortunately, due to the self-contained nature of machine learning models, the model can be run on-device without the need to access peripherals and system functions.

Principle 2: Enable Vendor Contributions to Span Ecosystem

Embedded devices come in all shapes and sizes, and require kernels to perform tinyML functions. The more optimized these kernels are for a particular device, the better performance will be achieved. However, because of the many differences between device platforms, there is no one-size-fits-all optimization solution. Consequently, the TFMicro team by itself is unable to support the wide variety of platforms that may want to run tinyML, and thus, vendors with strong motivation (i.e., those involved in microcontroller development) are encouraged to contribute to help bridge the gap. These vendors often have little experience with deep learning, and thus, TFMicro must provide sufficient resources to allow these teams to easily contribute. One way this is accomplished is by encouraging vendors to submit to a library repository and to provide tests and benchmarks for vendors to assess their hardware performance.

Principle 3: Reuse TensorFlow Tools for Scalability

The third principle focuses on scalability. More than 1,400 operations (e.g. CONV2D) are supported by TensorFlow and other machine learning training frameworks. However, inference frameworks (i.e., those actually deploying the model) typically only support a fraction of these operations. For most use-cases, this will likely not cause issues since the most commonly used operations will likely be supported, but this inherent difference leads to a mismatch between the set of potential models produced by the training framework and the set of potential models that can be deployed by the inference framework.

An exporter is used to convert a model from a training framework, such as TensorFlow, to a model for an inference framework, such as TFLite or TFLite for Microcontrollers. This model can then be deployed directly to a device and run using the library interpreter. Often, the training and inference frameworks are developed by different entities, which can present difficulties for developers when there are compatibility issues between the various stages of the developmental pipeline. This may render otherwise functional models unusable when trying to be deployed to a client device, especially when the incompatibilities are abstracted in high-level libraries such as Keras.

Due to these concerns, the TFMicro developers decided to reuse as many TensorFlow tools available as possible to help minimize such complications and compatibility issues.

Principle 4: Build System for Heterogeneous Support

The last principle focuses on promoting a flexible build environment. There are a large number of different types of embedded devices that may wish to use tinyML, and thus TFMicro should be designed without preference to any particular platform. This prevents vendor lock-in and also attracts a larger developer ecosystem due to improved portability. To combat this, TFMicro prioritizes code that can be built across a wide variety of integrated development environments (IDEs) and toolchains.

These four principles help to facilitate a developer ecosystem that is oriented towards maximizing portability between various hardware platforms, architectures, frameworks, and toolchains.
