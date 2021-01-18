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
* ABI = Application Binary Interface, which has the CPU instructions sets, endiannes of memory stores and loads at runtime \(Android is little-endian\), format of executable binaries \(Android uses ELF\)
* UID = User Identifier, used kernel for hierarchy access control. In Android each app gets its UID, as if each app would be a different user.
* OOM = undesired state of a computer when no additional memory can be allocated for use by programs or the OS.

### Linux Kernel

On the folder /boot in Ubuntu, is where the bootloader loads the kernel, the kernel is compressed and named as vmlinuz, if you want to check your kernel: $ uname -a There might be more than one kernel, in case one kernel breaks. To configure and customize our own kernel we have to download it separetely. To know [what is each file in /boot](https://www.linuxquestions.org/questions/linux-newbie-8/%5Bboot%5D-what-do-those-files-do-828407/) . The drivers \(called as modules in Kernel\), which are .c functions that makes interface with the hardware \(CPU and so on\) are located in the /lib/modules folder in Ubuntu.

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

#### _- Component Lifecycle_

Switching between components \(task\) sometimes can lead to the memory to be full and we have to manage the stack of components, so we have to take down a component so another one that the user is interested can be opened up, but when the user clicks on the taken down component, the previous state \(context\) should be saved as if he never closed it, to make this behaviour possible we use component lifecycle, which is basically callbacks for each component.

#### _- Manifest_

The main entry point of an app. Inform the system about the app's components, minimum API level required, HW requirements. It's an XML file \(like in ROS for ROS packages\) and resides on the top of the directory sources. Manifest \(components\) is statically declared \(at build time\), while broadcast receiver can be declared at runtime

#### _- Processes and Threads_

When an app's component is activated a process is started. Important to know is that more than one component is run within a single linux proccess, so if we make a long blocking operation on a standard component, we'll be running probably other components because the process is gonna run the other components, so in this case is better to use a Thread for it. \(low-memory conditions mindset\)

#### _- Remote Procedure Call \(RPC\)_

In order to components to communicate with each other, they do not use the traditional socket mechanism, but what is called as _binder_, which is a in-kernel binder mechanism, accessible through _/dev/binder._ But normal Android developers don't use the binder directly, they use the Android's Interface Definition Language \(IDL\). __

#### _- Security and Permissions_

As said in UID acronym, each app gets an UID. The "users"/apps can access other user's data only if granted \(hence iPhone, Android\) structure to ask if they can access your contact list or so. On the other hand, some apps can have the static declaration of access grant in the manifest file, like acessing the camera, location, internet \(sockets\)...

### SDK and NDK

Development: NDK and SDK. Native Development Kit, which CANNOT be confused to be an unlimited Development Kit, it is used mostly for graphics perfomance \(like games: Angry Birds, for instance\). But it goes indeed one layer down from the Java environment, here we can AS WELL program in C to interface with embedded systems, but it's not the focus, it still has its limitations. C -&gt; Java layer programming. When we want to add new functionality with new hardware then we have to use the NDK. Usually what happens is the programming in C and then when compiling the C code, we target the processor that we want to use \(arm64, for instance\) and then a .so Shared Object will be created, which basically has all functionalities from the c function embedded in a .so file along with the header file, making the code public and available to interface with Java, for example. Since the Android system already communicates properly with the chip, so the Java layer will communicate seamless with the compiled .so. For the supported processors, one has to [check the Android ABIs](https://developer.android.com/ndk/guides/abis).

Think about it: when we rewrite the kernel for a new purpose/ new android, we have to rewrite the SDK as well.

Features/drivers that have been added do the Linux Kernel to androidize \(important to say that those drivers \[at the time of writing of the book 2012 or 2013 maybe\] are located in the `drivers/staging/android`, because they have to be mature in order to be merged on the original kernel tree `drivers` \): 

* Wakelock: functionality that prevents the system going to low-power mode, useful because different from computers, smartphones need to be in an active state.
* Low-Memory Killer: kicks in before the OOM mechanism, the OOM only kicks in really when it's out of memory, but beforehand, Android deals with everything.
* Binder: remembering this is fundamental for components \(more specific: services\) to talk with each other \(RPC\) in the DevApp, which allows in the end apps to talk the System Server, hence what is used to make apps talk with each other. In the Linux philosophy if you want to add a new service, you would need to to implement a new daemon \(process\), with binder we can add remotely invocable objects, meaning we can implement the remote object in any desired language and share the same process space as other services. **Important to say that services used by System Server is not the same service by apps through the service component model, so to disguinsh both we say: service component and service. Services run with system privileges and live from boot to reboot, while service component are life-cycled components associated with the app and their app privileges. But binder interacts with both of them.** 

\_\_



