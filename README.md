
# 💡 Experiment 01 – Interfacing a Digital Output (LED) with ARM Development Board

### 🎯 **Aim**
To interface a digital output (LED) to an ARM development board and write a blink code.

---

### ⚙️ **Components Required**
- STM32CubeIDE  
- NUCLEO ARM Development Board  

---

### 🧠 **Theory**

**ARM (Advanced RISC Machine)** is a 32-bit processor architecture developed by ARM Holdings. It is widely used in embedded systems and SoC (System-on-Chip) products. Many semiconductor companies like Samsung, Atmel, and Texas Instruments license ARM architecture to design their own SoCs.
### 🧩 **What is an ARM7 Processor?**
The **ARM7 processor** is commonly used in embedded system applications. It provides a balance between the classic ARM architecture and the newer Cortex series, offering an excellent platform for both hardware and software development.
### 🔍 **LPC2148 Microcontroller**
The **LPC2148**, developed by NXP Semiconductors (Philips), is a 16/32-bit ARM7-based microcontroller featuring a wide range of peripherals.
#### **Key Features**
- 16/32-bit ARM7TDMI-S core in LQFP64 package  
- On-chip **Flash memory**: 32 KB – 512 KB  
- On-chip **SRAM**: 8 KB – 40 KB  
- **ISP/IAP** via on-chip bootloader  
- **Embedded ICE-RT** and **Real Monitor** for real-time debugging  
- **USB 2.0** full-speed device controller with 2 KB endpoint RAM  
- **10-bit ADC** (6 or 14 channels, 2.44 μs conversion time)  
- **10-bit DAC** for analog output  
- **Timers:** Two 32-bit timers, watchdog, and PWM unit  
- **RTC** with 32 kHz clock input  
- **UARTs (2x), I²C (2x)** up to 400 kbit/s  
- **5V-tolerant GPIOs**, 21 external interrupt pins  
- **Max CPU Clock:** 60 MHz using on-chip PLL (lock time 100 µs)  
- **Crystal Frequency:** 1 MHz – 25 MHz  
- **Power modes:** Idle and Power-down with peripheral clock scaling  

---

### 🧭 **Procedure**

1. Open **STM32CubeIDE**.
   <img width="1050" height="591" alt="image" src="https://github.com/user-attachments/assets/109135f6-e6f9-46f8-86e1-ecafa6170b01" />

2. Click **File → New STM32 Project**.
   <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/a5799efb-57e1-42b8-ba46-b09f32d86fcb" />
<img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/edf33429-8eea-4857-a991-c2d7706fc787" />

3. Select the **target microcontroller** or board and click **Next**.
   <img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/f93d88b6-cd7f-49db-84de-351f9b116488" />

4. Name the project.
   <img width="533" height="588" alt="image" src="https://github.com/user-attachments/assets/63de2bab-69d4-4cb9-8db6-1b57adff9878" />
![Blink 1](https://github.com/user-attachments/assets/f101c399-39a9-4735-bcc2-7b600245d729)



5. The corresponding `.ioc` file will be generated automatically.
  <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/8900847c-6745-43e2-9ecf-2e66877fdc49" />

![blink 2](https://github.com/user-attachments/assets/66255181-38cc-4a30-9df2-f372d6758191)


6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
   <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/acc4f1c4-5e33-431b-8a76-3b102016baa6" />
<img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/b7abcd80-797d-451f-a7c3-23f303822423" />

![blink 2](https://github.com/user-attachments/assets/e331718f-e2bd-41f2-9e85-c8276266d2dc)



7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
   <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/dbf4b205-5db9-4e9b-8150-94f441c8b116" />

![blink 2](https://github.com/user-attachments/assets/31e6cb81-3dc9-450d-8ef6-71c36d3bea0a)

 
8. Edit the generated main program as required.
   <img width="1110" height="624" alt="image" src="https://github.com/user-attachments/assets/05b39060-35d6-420d-9f4d-8721439bd82f" />
<img width="1104" height="621" alt="image" src="https://github.com/user-attachments/assets/2ec55709-a45f-4e6e-8738-6aa94138eab1" />

![blink 8](https://github.com/user-attachments/assets/89919f16-98ec-47a5-b0c7-d647c654a39b)


9. Click **Project → Build All**.
    <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/264cd0a8-3e96-4668-822e-838ecfafc527" />

![blink 10](https://github.com/user-attachments/assets/b50742e1-86a1-4796-a2ac-cd18f63b5e60)

10. Link the **HEX file** using the post-build process.
    <img width="1053" height="465" alt="image" src="https://github.com/user-attachments/assets/478187a0-0ee6-4c50-9cac-c3b5ee18521b" />

11. Click **Debug** and connect the **STM Nucleo Board**.
    <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/f72fff44-6073-4ae4-aa78-0da455df9af1" />

13. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);
        HAL_Delay(1000);
        HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
        HAL_Delay(1000);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 
<img width="1056" height="792" alt="image" src="https://github.com/user-attachments/assets/cafad25b-eae9-4970-afd3-8cb874a1ae6a" />

CASE 2: LED OFF
<img width="1056" height="792" alt="image" src="https://github.com/user-attachments/assets/4c803807-51c1-427f-9ea2-8f9982e3adc1" />


---
### RESULT
Interfacing a digital output with ARM microcontroller is executed and the results are verified.
