#include "FreeRTOS.h"
#include "task.h"
#include <stdio.h>

/* Task Function Prototypes */
void LED_Task(void *pvParameters);
void Print_Task(void *pvParameters);

int main(void)
{
    /* Create LED Task */
    xTaskCreate(
        LED_Task,
        "LED Task",
        1000,
        NULL,
        1,
        NULL
    );

    /* Create Print Task */
    xTaskCreate(
        Print_Task,
        "Print Task",
        1000,
        NULL,
        1,
        NULL
    );

    /* Start Scheduler */
    vTaskStartScheduler();

    while(1);
}

/* LED Blinking Task */
void LED_Task(void *pvParameters)
{
    while(1)
    {
        printf("LED ON\n");
        vTaskDelay(pdMS_TO_TICKS(500));

        printf("LED OFF\n");
        vTaskDelay(pdMS_TO_TICKS(500));
    }
}

/* Message Printing Task */
void Print_Task(void *pvParameters)
{
    while(1)
    {
        printf("RTOS Task Running...\n");

        vTaskDelay(pdMS_TO_TICKS(1000));
    }
}
