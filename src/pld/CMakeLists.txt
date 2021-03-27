add_library(pld STATIC
	pld.c
	virtex2.c
	xilinx_bit.c)

set_property(TARGET pld PROPERTY POSITION_INDEPENDENT_CODE ON)
