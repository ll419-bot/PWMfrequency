# PWMfrequency
ARR:
ARR 决定了 PWM 信号的 周期（频率）
ARR = (定时器时钟频率 / (预分频系数 + 1) / 目标频率) - 1
在stm32g4rbt6中 定时器时钟频率一般为80MHZ 预分频系数的英文单词是pcr

CCR:
CCR 决定了 PWM 信号的 占空比（高电平时间占周期的比例）
CCR = 占空比 × (ARR + 1)
占空比其实就是高电平的时间

HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_2);
	TIM2->CCR2 = 50;
	





