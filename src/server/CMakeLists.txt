add_library(server STATIC
	server.c
	telnet_server.c
	gdb_server.c
	server_stubs.c
	tcl_server.c)

set_property(TARGET server PROPERTY POSITION_INDEPENDENT_CODE ON)
