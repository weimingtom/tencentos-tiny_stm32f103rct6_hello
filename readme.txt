#define B1_Pin GPIO_PIN_13 //KEY1=PC13, KEY0=PC1
#define B1_GPIO_Port GPIOC
#define LD2_Pin GPIO_PIN_2 //D2=PD2, D1=VCC
#define LD2_GPIO_Port GPIOD 

---------------------

//use UART1 or UART2 as debug serial ?
#define USART_DEBUG 1

#if USART_DEBUG == 1
/*use uart1 as debug uart*/
#define USART_DEBUG_PORT USART1
#elif USART_DEBUG == 2
/*use uart2 as debug uart*/
#define USART_DEBUG_PORT USART2
#endif

-------------------

void task1(void *arg)
{
    int count = 1;
    while (1) {
      HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);  //TODO: added, turn LD2 off or on
      
      
--------------------

  /*Configure GPIO pin Output Level, LD2 */
  //HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_RESET); //turn LD2 on
  HAL_GPIO_WritePin(LD2_GPIO_Port, LD2_Pin, GPIO_PIN_SET); //turn LD2 off
  
--------------------




void MX_USART2_UART_Init(void)
{

  huart_0.Instance = USART_DEBUG_PORT;
  huart_0.Init.BaudRate = 115200;
  huart_0.Init.WordLength = UART_WORDLENGTH_8B;
  huart_0.Init.StopBits = UART_STOPBITS_1;
  huart_0.Init.Parity = UART_PARITY_NONE;
  huart_0.Init.Mode = UART_MODE_TX_RX;
  huart_0.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart_0.Init.OverSampling = UART_OVERSAMPLING_16;
  if (HAL_UART_Init(&huart_0) != HAL_OK)
  {
    Error_Handler();
  }

}

void HAL_UART_MspInit(UART_HandleTypeDef* uartHandle)
{

  GPIO_InitTypeDef GPIO_InitStruct = {0};
	if(uartHandle->Instance==USART1)
	{
    __HAL_RCC_USART1_CLK_ENABLE();
  
    __HAL_RCC_GPIOA_CLK_ENABLE();
    /**USART1 GPIO Configuration    
    PA9     ------> USART1_TX
    PA10     ------> USART1_RX 
    */
    GPIO_InitStruct.Pin = GPIO_PIN_9 | GPIO_PIN_10;
    GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);	
	}
  if(uartHandle->Instance==USART2)
  {
  /* USER CODE BEGIN USART2_MspInit 0 */

  /* USER CODE END USART2_MspInit 0 */
    /* USART2 clock enable */
    __HAL_RCC_USART2_CLK_ENABLE();
  
    __HAL_RCC_GPIOA_CLK_ENABLE();
    /**USART2 GPIO Configuration    
    PA2     ------> USART2_TX
    PA3     ------> USART2_RX 
    */
    GPIO_InitStruct.Pin = GPIO_PIN_2 | GPIO_PIN_3;
    GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  /* USER CODE BEGIN USART2_MspInit 1 */

  /* USER CODE END USART2_MspInit 1 */
  }
}

void HAL_UART_MspDeInit(UART_HandleTypeDef* uartHandle)
{
  if(uartHandle->Instance==USART1)
  {
    __HAL_RCC_USART1_CLK_DISABLE();
  
    /**USART1 GPIO Configuration    
    PA9     ------> USART1_TX
    PA10     ------> USART1_RX 
    */
    HAL_GPIO_DeInit(GPIOA, GPIO_PIN_9 | GPIO_PIN_10);
  }
  if(uartHandle->Instance==USART2)
  {
  /* USER CODE BEGIN USART2_MspDeInit 0 */

  /* USER CODE END USART2_MspDeInit 0 */
    /* Peripheral clock disable */
    __HAL_RCC_USART2_CLK_DISABLE();
  
    /**USART2 GPIO Configuration    
    PA2     ------> USART2_TX
    PA3     ------> USART2_RX 
    */
    HAL_GPIO_DeInit(GPIOA, GPIO_PIN_2 | GPIO_PIN_3);

  /* USER CODE BEGIN USART2_MspDeInit 1 */

  /* USER CODE END USART2_MspDeInit 1 */
  }
} 

---------------------------------

