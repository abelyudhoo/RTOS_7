# LED Control RTOS Application

This project demonstrates an LED control system implemented using **FreeRTOS** on an STM32 microcontroller. The application consists of multiple tasks that control different LEDs, simulating concurrent behavior with critical sections and delays.  


https://github.com/user-attachments/assets/d7e8b401-34ff-4471-8bad-774a98ee57dd


## Features

- **Green LED Task**: Toggles a green LED with a periodic delay and safely accesses shared data using critical sections.
- **Red LED Task**: Toggles a red LED at a different periodic rate, also using critical sections to access shared data.
- **Orange LED Task**: Continuously toggles an orange LED without accessing shared resources.
- **Default Task**: A placeholder task that runs periodically.

### Highlights
- **Real-Time Operating System (RTOS)**: Implemented with FreeRTOS for task scheduling.
- **Shared Data Protection**: Critical sections (`taskENTER_CRITICAL` and `taskEXIT_CRITICAL`) are used to manage access to shared resources.
- **Simulated Read/Write**: Mimics read/write operations on shared data with delays to emulate real-world scenarios.

---

## System Requirements

- **Microcontroller**: STM32 (configured for HSI clock source).
- **Development Environment**: STM32CubeIDE.
- **FreeRTOS**: Included in the project setup.
- **Hardware**:
  - STM32 board with GPIO pins connected to LEDs.
  - At least three GPIO pins for the Green, Red, and Orange LEDs.

---

## GPIO Configuration

| **LED**        | **GPIO Pin** |
|-----------------|--------------|
| Green LED       | GPIO_PIN_0   |
| Red LED         | GPIO_PIN_1   |
| Orange LED      | GPIO_PIN_3   |
| Shared Resource | GPIO_PIN_2   |

---

## Task Overview

| **Task Name**       | **Function**       | **Priority**       | **Stack Size** | **Details**                     |
|----------------------|--------------------|--------------------|----------------|----------------------------------|
| `defaultTask`       | `StartDefaultTask` | Normal             | 128            | Runs periodically with no action. |
| `HijauLedTask`      | `GreenLedTask`     | Normal             | 128            | Toggles the green LED with critical section handling. |
| `MerahLedTask`      | `RedLedTask`       | Normal             | 128            | Toggles the red LED with critical section handling. |
| `OrenLedTask`       | `OrangeLedTask`    | Above Normal       | 128            | Continuously toggles the orange LED. |

---

## How to Build and Run

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/led-control-rtos.git
   ```
2. **Open Project in STM32CubeIDE**:
   - Import the project into STM32CubeIDE.
   - Ensure FreeRTOS middleware is enabled.
3. **Compile the Code**:
   - Build the project.
   - Ensure there are no errors during compilation.
4. **Flash the Microcontroller**:
   - Connect the STM32 board via USB.
   - Flash the firmware using the STM32CubeIDE debugger or ST-Link.
5. **Run the Application**:
   - Observe the LEDs toggling as per the task behaviors.

---

## File Structure

```
├── Core
│   ├── Inc
│   │   ├── main.h                # Main header file
│   ├── Src
│   │   ├── main.c                # Main application file
│   │   ├── stm32f4xx_it.c        # Interrupt handlers
│   │   ├── freertos.c            # FreeRTOS configuration
├── Drivers
│   ├── HAL_Drivers               # HAL libraries for STM32
├── LICENSE                       # Project license
├── README.md                     # This file
```

---

## Key Functions

- **`accessSharedData()`**:  
  Handles access to a shared variable (`startFlag`) and toggles a GPIO pin (shared resource).  
  Includes simulated delay via `SimulateReadWriteOperation()` to emulate read/write operations.

- **`SimulateReadWriteOperation()`**:  
  Introduces a delay using a simple `for` loop to simulate a blocking operation.
