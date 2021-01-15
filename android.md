---
description: Personal notes about Embedded Android.
---

# Android

### Acronyms/Terms:

* HAL = Hardware Abstraction Layer
* AOSP = Android Open Source Project = Android Platform
* Android compatible Linux Kernel
* SoC = System On A Chip
* Dalvik = custom build VM for running Android so it doesn't use proprietary material from Oracle \(Java\)
* Apache Harmony = instead of the official class library, it's a reimplementation of the class lib.

### Linux Kernel

Na pasta /boot do linux, é onde o bootloader carrega o kernel. \(vmlinuz\) $ uname -a. Pode haver mais de um kernel, caso um quebre, escolhemos outro que funcione. Lembrando que esse kernel é compressed, então não temos acesso a ele. Para acessar e ver como configurar o kernel, baixamos do site. To know [what is each file in /boot](https://www.linuxquestions.org/questions/linux-newbie-8/%5Bboot%5D-what-do-those-files-do-828407/) . The drivers \(called as modules in Kernel\), which are .c functions that makes interface with the hardware \(CPU and so on\) are located in the /lib/modules folder in Ubuntu.

By configuring the kernel using libncurses5-dev \(which is a text based GUI\) we can easily setup our kernel the way we want, for instance: I want to enable Windows file type system to our kernel, then we can make the change on it and we select if we want to ocnfig the knowledge to be loaded in the kernel only when needed \(M, as module\) or always \(\*\)..

### Android App Developer's View

The entire Android behavior is predicted on low-memory conditions. Concepts that are important to understand, even though i'm focused on embedded systems. 

#### - Components

There's no main\(\) function in Android apps, applications consist of components and one component from an app can invoke or use component of other apps. Instead of main function, there are predefined events, called intents in which developers can tie their components to, therefore enabling the components to be activated on the occurrence of other events. Example: pressing the Contacts button in the Dialer app opens up the component Contacts.

Types of components:

* Activities: it's like a web browser tab window, but in this case activities can't be resized/maximized/minimized, they always take the entire space, using the back button to navitage throug them. One activity can be displayed as an icon on the Android homescreen. A stack of activities is called a task.
* Services: are like daemons in Unix \(background process\). Service is activated when a component requests it.
* Broadcast receiver: interrupt handlers or like trigger event, sensitive to a specific matter.
* Content provider: database for the app. Most content providers rely on SQLite, which is included in Android.

#### - Intents

Allows components to interact. Is a passive object, what matters for the interaction is actually the dispatching \(and its contents\) and the mechanism to dispatch it \(along with system built-in rules etc\). _Example of system rule: intents are tied to the type of the component they are sent to, intent sent by a service can be only received by a service, not by a broadcaster or activity._ 

#### - Component Lifecycle

Switching between components \(task\) sometimes can lead to the memory to be full and we have to manage the stack of components, so we have to take down a component so another one that the user is interested can be opened up, but when the user clicks on the taken down component, the previous state \(context\) should be saved as if he never closed it, to make this behaviour possible we use component lifecycle, which is basically callbacks for each component.

#### - Manifest

The main entry point of an app. Inform the system about the app's components, minimum API level required, HW requirements. It's an XML file \(like in ROS for ROS packages\) and resides on the top of the directory sources. Manifest \(components\) is statically declared \(at build time\), while broadcast receiver can be declared at runtime

#### - Processes and Threads

When an app's component is activated a process is started. Important to know is that more than one component is run within a single linux proccess, so if we make a long blocking operation on a standard component, we'll be running probably other components because the process is gonna run the other components, so in this case is better to use a Thread for it. \(low-memory conditions mindset\)

#### - Remote Procedure Call \(RPC\)

In order to components to communicate with each other, they do not use the traditional socket mechanism, but what is called as _binder_, which is a in-kernel binder mechanism, accessible through _/dev/binder._ But normal Android developers don't use the binder directly, they use the Android's Interface Definition Language \(IDL\). __

\_\_

Development: NDK and SDK. Native Development Kit, which stands for the C -&gt; Java layer programming. When we want to add new functionality with new hardware then we have to use the NDK. Usually what happens is the programming in C and then when compiling the C code, we target the processor that we want to use \(arm64, for instance\) and then a .so Shared Object will be created, which basically has all functionalities from the c function embedded in a .so file along with the header file, making the code public and available to interface with Java, for example. Since the Android system already communicates properly with the chip, so the Java layer will communicate seamless with the compiled .so. 

Think about it: when we rewrite the kernel for a new purpose/ new android, we have to rewrite the SDK as well.

\_\_



