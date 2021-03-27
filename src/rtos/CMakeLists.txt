add_library(rtos STATIC
	chibios.c
	chromium-ec.c
	eCos.c
	embKernel.c
	FreeRTOS.c
	hwthread.c
	linux.c
	mqx.c
	nuttx.c
	riot.c
	rtos.c
	rtos_chibios_stackings.c
	rtos_ecos_stackings.c
	rtos_embkernel_stackings.c
	rtos_mqx_stackings.c
	rtos_riot_stackings.c
	rtos_standard_stackings.c
	rtos_ucos_iii_stackings.c
	ThreadX.c
	uCOS-III.c)

