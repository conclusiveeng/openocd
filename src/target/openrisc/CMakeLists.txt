add_library(openrisc STATIC
	or1k.c
	or1k_du_adv.c
	or1k_tap_mohor.c
	or1k_tap_vjtag.c
	or1k_tap_xilinx_bscan.c
	jsp_server.c)

set_property(TARGET openrisc PROPERTY POSITION_INDEPENDENT_CODE ON)
