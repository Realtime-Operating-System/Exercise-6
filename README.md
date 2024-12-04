# STM32 FreeRTOS LED Task with Critical Section

This project demonstrates how to use FreeRTOS with critical sections to eliminate resource contention in an STM32F401 microcontroller. By suspending the scheduler during access to shared resources, this exercise ensures that interference (collisions) between tasks is avoided.

## Features
- **RTOS**: FreeRTOS with critical section implementation.
- **Collision-Free Shared Access**: Ensures no interference occurs during shared resource access.
- **LED Control**:
  - Green LED: Controlled by a normal-priority task, toggles every 500 ms.
  - Red LED: Controlled by an above-normal-priority task, toggles every 100 ms.
  - Blue LED: Previously used to indicate collisions, now remains off.
- **Critical Sections**:
  - Scheduler suspension using `taskENTER_CRITICAL` and `taskEXIT_CRITICAL` ensures mutual exclusion.

## Hardware Requirements
- **Microcontroller**: STM32F401.
- **LEDs**:
  - Green LED: Connected to PA5.
  - Red LED: Connected to PB0.
  - Blue LED: Connected to PB7.
- **IDE/Toolchain**: STM32CubeMX, STM32CubeIDE, or any supported ARM GCC toolchain.

## Software Requirements
- **HAL Library**: STM32 HAL library for GPIO and system configuration.
- **FreeRTOS**: Real-Time Operating System for task scheduling.

## Circuit Description
- **Green LED**: Pin PA5 toggles every 500 ms, controlled by a low-priority task.
- **Red LED**: Pin PB0 toggles every 100 ms, controlled by a higher-priority task.
- **Blue LED**: Pin PB7 used to indicate collisions, which no longer occur.
- Pull-down resistors are used to stabilize LED states, with negative pins connected to ground.

## How It Works

### 1. Green LED Task (Normal Priority)
- The task toggles the green LED every 500 ms.
- Represents a lower-priority task, preempted by the Red LED Task when it becomes ready.
- Implements critical sections to ensure collision-free shared access.

### 2. Red LED Task (Above-Normal Priority)
- The task toggles the red LED every 100 ms.
- Represents a higher-priority task that preempts the Green LED Task.
- Implements critical sections to ensure collision-free shared access.

### 3. Critical Sections
- Shared data is accessed inside critical sections.
- Critical sections use the following FreeRTOS APIs:
  - **Disable interrupts**: `taskENTER_CRITICAL();`
  - **Enable interrupts**: `taskEXIT_CRITICAL();`
- By disabling and re-enabling interrupts, tasks ensure mutual exclusion, preventing resource contention.

### 4. Scheduler
- The FreeRTOS kernel handles task scheduling based on priority.
- The Green and Red LED tasks access shared resources without interference, thanks to critical sections.

## Steps to Run the Program

### 1. Setup STM32CubeMX
- Select the STM32F401 microcontroller.
- Enable GPIO pins for PA5, PB0, and PB7.
- Enable FreeRTOS middleware.

### 2. Configure Tasks
- Add two tasks:
  - **FlashGreenLEDTask**: Normal priority, toggles the green LED.
  - **FlashRedLEDTask**: Above-normal priority, toggles the red LED.

### 3. Add Critical Sections
- Wrap shared resource access in each task with `taskENTER_CRITICAL` and `taskEXIT_CRITICAL` to suspend and resume the scheduler.

### 4. Generate Code
- Generate project code for STM32CubeIDE or your preferred IDE.

### 5. Build and Flash
- Build the project and flash it to the STM32F401 using an ST-Link or compatible programmer.

### 6. Observe Behavior
- The Green and Red LEDs blink at their respective intervals without interference.
- The Blue LED remains off, confirming that no collisions occur during shared resource access.

---
## Circuit Form
![rangkaian task indicator](https://github.com/user-attachments/assets/2adc1669-8599-47b5-87c8-a6995886f812)

## Demo Video
[task_indicator2](https://github.com/user-attachments/assets/8c15592a-bab7-4cc4-b6ee-1da58e3713b1)

