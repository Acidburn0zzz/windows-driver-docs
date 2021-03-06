---
title: Introduction to Standard Driver Routines
author: windows-driver-content
description: Introduction to Standard Driver Routines
ms.assetid: 91aaca02-a571-4058-b5af-98277fcbcf9d
keywords: ["standard driver routines WDK kernel , about standard driver routines", "driver routines WDK kernel , about standard driver routines", "routines WDK kernel , about standard driver routines", "IRPs WDK kernel , standard driver routines", "required standard routines WDK kernel", "optional standard routines WDK kernel"]
ms.date: 06/16/2017
ms.localizationpriority: medium
---

# Introduction to Standard Driver Routines





Each kernel-mode driver is constructed around a set of system-defined, [standard driver routines](https://msdn.microsoft.com/library/windows/hardware/ff563842). Kernel-mode drivers process *I/O request packets* (IRPs) within these standard routines by calling system-supplied driver support routines.

All drivers, regardless of their level in a chain of attached drivers, must have a basic set of standard routines in order to process IRPs. Whether a driver must implement additional standard routines depends on whether the driver controls a physical device or is layered over a physical device driver, as well as on the nature of the underlying physical device. Lowest-level drivers that control physical devices have more required routines than higher-level drivers, which typically pass IRPs to a lower driver for processing.

Standard driver routines can be divided into two groups: those that each kernel-mode driver must have, and those that are optional, depending on the driver type and location in the [*device stack*](https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-stack).

This section describes required standard routines. Other sections describe the optional routines.

Following are two tables. The first table lists required standard routines. The second lists most of the optional routines.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Required standard driver routines</th>
<th>Purpose</th>
<th>Where described</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DriverEntry</strong></p></td>
<td><p>Initializes the driver and its driver object.</p></td>
<td><p>[Writing a DriverEntry Routine](writing-a-driverentry-routine.md)</p></td>
</tr>
<tr class="even">
<td><p><em>AddDevice</em></p></td>
<td><p>Initializes devices and creates device objects.</p></td>
<td><p>[Writing an AddDevice Routine](writing-an-adddevice-routine.md)</p></td>
</tr>
<tr class="odd">
<td><p>Dispatch Routines</p></td>
<td><p>Receive and process IRPs.</p></td>
<td><p>[Writing Dispatch Routines](writing-dispatch-routines.md)</p></td>
</tr>
<tr class="even">
<td><p><em>Unload</em></p></td>
<td><p>Release system resources acquired by the driver.</p></td>
<td><p>[Writing an Unload Routine](writing-an-unload-routine.md)</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Optional standard driver routines</th>
<th>Purpose</th>
<th>Where described</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Reinitialize</em></p></td>
<td><p>Completes driver initialization if <strong>DriverEntry</strong> cannot.</p></td>
<td><p>[Writing a Reinitialize Routine](writing-a-reinitialize-routine.md)</p></td>
</tr>
<tr class="even">
<td><p><em>StartIo</em></p></td>
<td><p>Starts an I/O operation on a physical device.</p></td>
<td><p>[Writing a StartIo Routine](writing-a-startio-routine.md)</p></td>
</tr>
<tr class="odd">
<td><p>Interrupt Service Routine</p></td>
<td><p>Saves the state of a device when it interrupts.</p></td>
<td><p>[Writing an ISR](writing-an-isr.md)</p></td>
</tr>
<tr class="even">
<td><p>Deferred Procedure Calls</p></td>
<td><p>Completes the processing of a device interrupt after an ISR saves the device state.</p></td>
<td><p>[DPC Objects and DPCs](dpc-objects-and-dpcs.md)</p></td>
</tr>
<tr class="odd">
<td><p><em>SynchCritSection</em></p></td>
<td><p>Synchronizes access to driver data.</p></td>
<td><p>[Using Critical Sections](using-critical-sections.md)</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterControl</em></p></td>
<td><p>Initiates DMA operations.</p></td>
<td><p>[Adapter Objects and DMA](adapter-objects-and-dma.md)</p></td>
</tr>
<tr class="odd">
<td><p><em>IoCompletion</em></p></td>
<td><p>Completes a driver's processing of an IRP.</p></td>
<td><p>[Completing IRPs](completing-irps.md)</p></td>
</tr>
<tr class="even">
<td><p><em>Cancel</em></p></td>
<td><p>Cancels a driver's processing of an IRP.</p></td>
<td><p>[Canceling IRPs](canceling-irps.md)</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomTimerDpc</em>, <em>IoTimer</em></p></td>
<td><p>Timing and synchronizing events.</p></td>
<td><p>[Synchronization Techniques](synchronization-techniques.md)</p></td>
</tr>
</tbody>
</table>

 

The current IRP and target device object are input parameters to many standard routines. Every driver processes each IRP in stages through its set of standard routines.

By convention, the system-supplied drivers prepend an identifying, driver-specific or device-specific prefix to the name of every standard routine except **DriverEntry**. As an example, this documentation uses "DD", as shown in the [driver object illustration](introduction-to-driver-objects.md#driver-object-illustration). Following this convention makes it easier to debug and maintain drivers.

 

 




