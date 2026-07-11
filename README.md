# STM32-G474RE-GPIO-Button-LED

Project Overview

This project demonstrates basic GPIO input and output control using the NUCLEO-G474RE development board.

The onboard user button is used as a GPIO input, and the onboard LED is used as a GPIO output.

When the user presses the button, the LED state changes.

Hardware
STM32 NUCLEO-G474RE development board
USB cable
Onboard user button B1
Onboard LED LD2
Software
STM32CubeIDE
STM32CubeMX
STM32 HAL Library
GPIO Configuration
Component	GPIO Mode	Description
User Button B1	GPIO Input	Reads the button state
LED LD2	GPIO Output	Controls the LED state

The exact GPIO pins are configured in the STM32CubeIDE .ioc file.

Main Functions

The project mainly uses the following STM32 HAL GPIO functions:

HAL_GPIO_ReadPin();
HAL_GPIO_WritePin();
HAL_GPIO_TogglePin();
Read Button State
GPIO_PinState current_button_state;

current_button_state =
    HAL_GPIO_ReadPin(USER_BUTTON_GPIO_Port, USER_BUTTON_Pin);
Turn LED On or Off
HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET);

HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET);
Toggle LED State
HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);
Project Function

The program continuously reads the state of the user button.

When a valid button press is detected, the program toggles the onboard LED.

A simple delay can be used for button debounce to prevent one button press from being detected multiple times.

Example:

if (HAL_GPIO_ReadPin(USER_BUTTON_GPIO_Port,
                     USER_BUTTON_Pin) == GPIO_PIN_RESET)
{
    HAL_Delay(20);

    if (HAL_GPIO_ReadPin(USER_BUTTON_GPIO_Port,
                         USER_BUTTON_Pin) == GPIO_PIN_RESET)
    {
        HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);

        while (HAL_GPIO_ReadPin(USER_BUTTON_GPIO_Port,
                                USER_BUTTON_Pin) == GPIO_PIN_RESET)
        {
        }
    }
}
How to Build and Run
Open STM32CubeIDE.
Select File → Import.
Import the existing STM32 project.
Connect the NUCLEO-G474RE board using a USB cable.
Build the project using:
Ctrl + B
Click Run or Debug to download the program to the board.
Press the onboard user button and observe the LED.
Project Structure
Core/
├── Inc/
│   └── main.h
└── Src/
    └── main.c

Drivers/
Demo/
Images/
Project_Name.ioc
README.md
Demo

The demonstration video is available in the Demo folder.

Demo/button_led_demo.mp4
Learning Objectives

Through this project, I learned:

How to create an STM32CubeIDE project
How to configure GPIO input and output
How to read a digital input signal
How to control a digital output
How to use STM32 HAL GPIO functions
How to implement simple button debounce
How to build and download an STM32 project
Future Improvements

Possible improvements include:

Using GPIO external interrupts instead of polling
Implementing a state machine
Supporting short press and long press
Controlling different LED blinking modes
Using a timer for non-blocking debounce
