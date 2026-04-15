# g491-01-blink-uart-debug
Simple project for STM32G491RET6 with a blink loop and logging using LPUART

Following the schematics for the STM32G491RET6 device, I have assigned GPIO_Output to PA5 which controls the LD2 (refer to image below)

<img width="845" height="568" alt="Captura de pantalla 2026-04-15 a las 14 24 50" src="https://github.com/user-attachments/assets/e5c04b13-4140-43e4-ac14-9d6c0b33e396" />

For the logging I have used LPUART1, which is by default connected to the STLINK-V3E Virtual COM port. This requires PA2 to be assigned as LPUART1_TX and PA3 as LPUART2_TX:
<img width="829" height="195" alt="Captura de pantalla 2026-04-15 a las 14 27 32" src="https://github.com/user-attachments/assets/12aba53d-79af-4236-8767-bd6900de7d9e" />

Inside the main.h file I have added two functions:
  - blink, which just sets and resets the value of PA5 (LD2) with 1 second intervals
  - log_uart, which uses the built in HAL_UART_Transmit function to transmit a message. This function logs the initialization of the LPUART, the end of the system boot (after HAL_Init() executes, the flash, clock, GPIO and UART are initialized) and then in the blink function it serves as a simple log to indicate when the LD2 turns on and off.

I have modified the baud rate to 9600, as it is a common value for LPUART.
