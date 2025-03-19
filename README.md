# PWMfrequency
ARR:
ARR 决定了 PWM 信号的 周期（频率）
ARR = (定时器时钟频率 / (预分频系数 + 1) / 目标频率) - 1
在stm32g4rbt6中 定时器时钟频率一般为80MHZ 预分频系数的英文单词是pcr

CCR:
CCR 决定了 PWM 信号的 占空比（高电平时间占周期的比例）
CCR = 占空比 × (ARR + 1)
占空比其实就是高电平的时间

在cubemx里面配置的时候 CH Polarity这个选项表示通道极性 有两种极性 一个是高 另一个是低
当有 “​High”（高电平）​时
表示 ​有效电平为高电平​（Active High）。当 PWM 处于有效状态时（例如计数器值 < CCR），输出高电平；否则输出低电平。

关于占空比的计算 与上面这个 CH Polarity 有关          也与这个有关 1.向上计数模式  2.PWM模式1
当ARR = 249 → 周期为 ARR + 1 = 250 个计数周期
（计数器从 0 递增到 249，共 250 个计数值）
​CCR2 = 50 → 当 CNT < 50 时输出有效电平（低电平），否则输出无效电平（高电平）

HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_2);   //开启pwm模式
	
	所以
​高电平占空比​（有效电平占比）：（50 / 250 ）*100% = 20%
​低电平占空比​（无效电平占比）： （200 /250） *100% =80%

占空比默认指有效电平占比，因此答案为 20%。
若需低电平占比，需明确指定，结果为 ​80%。

 uint16_t PA6_frq,PA7_frq;
 uint8_t  PA6_duty = 10,PA7_duty = 10;
 
TIM16->CCR1= PA6_duty;
 TIM17->CCR1 = PA7_duty;
 
if(key_down==3)
	  {
		  PA6_duty +=10;
		  if(PA6_duty==100) PA6_duty=10;
		  TIM16->CCR1 = PA6_duty;
	  }


