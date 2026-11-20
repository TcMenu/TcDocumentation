+++
title = "Task Manager - Using Spin Locks and provided Atomics"
description = ""
tags = "arduino, library, event-based"
date = "2021-04-20"
author =  "dave"
githublink = "https://github.com/TcMenu/TaskManagerIO"
referenceDocs = "/taskmanagerio/html/index.html"
banner = "/images/electronics/arduino/taskmgr/taskmanager-marshalling-interrupt.png"
toc_needed = true
type ="blog"
weight = 5
+++

## TaskManager provided spin locking

Before using any atomics always call `tmInitAtomics();`

Task Manager supports the concept of Spin Locks to protect sensitive asynchronous operations  from becoming interleaved. For example, to protect sensitive blocks of code. In all supported cases this includes memory safety between the threads. NEVER use this in an interrupt, prefer using TaskManager events for that instead. 

A spin lock loops waiting for the lock to become available, you can either spin for a period of time, or until the lock is acquired. While waiting for the lock in the spin, TASKS DO NOT RUN, and you must **never call yieldForMicros while holding a lock.** It is designed for very short locking operations in microseconds.

The `TmSpinLock` class provides a C++ RAII wrapper around an atomic boolean variable. You should globally create an atomic boolean variable as shown below:

    tm_internal::TmAtomicBool myLockBool;

Then during initialization set it to `false`:

    void setup() {
        atomicWriteBool(&myLockBool, false); 
    }

Then when you want to lock:

    void somethingNeedingLock() {
        tm_internal::TmSpinLock lock(&myLockBool);
        // any code in the same block is locked as per RAII standard.
    }


## A quick summary of atomic types within taskmanager

In the embedded domain, not all boards support lock free integers. Even some that do, either don't support `std::atomic` or don't support it fully. This leaves us having to provide standardized calls for booleans, integers, and pointers, that work everywhere. TaskManager provides a lock and limited atomic variable types that work on a wide range of boards. 

In the main [Arduino Libraries page](${relRef("arduino-libraries.md")}) we discuss all the supported platforms and how atomics are implemented on each. But here we describe the usage.

Before using any atomics always call `tmInitAtomics();`

For all the below assume `using namespace tm_internal`:

### TmAtomicBool - atomic boolean for all platforms

Except on AVR this is implemented as 32 bit.

    tm_internal::TmAtomicBool myLockBool;       // create atomic boolean variable
    bool atomicReadBool(&myLockBool)            // read value
    void atomicWriteBool(&myLockBool, newVal)   // write value
    // wraps CAS operation for all boards (only apply newVal if memory matches expected)
    // return value is true if swapped, otherwise false
    bool atomicSwapBool(&myLockBool, expected, newVal)  

### TmAtomicUInt32 - atomic integer for all platforms

On all platforms this is a 32 unsigned integer.

    tm_internal::TmAtomicUInt32 myLockInt;     // create atomic uint32 variable
    uint32_t atomicRead32(&myLockInt)          // read value
    void atomicWrite32(&myLockInt, newVal)     // write value
    // wraps CAS operation for all boards (only apply newVal if memory matches expected)
    // return value is true if swapped, otherwise false
    bool atomicSwap32(&myLockInt, expected, newVal)

## General notes

Code completely outside of task manager can use these constructs.

Be aware that these atomics and locks have limitations. For locks, keep the time locked to an absolute minimum and follow the guide above carefully.
