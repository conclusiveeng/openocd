add_subdirectory(aice)
add_subdirectory(drivers)
add_subdirectory(hla)
add_subdirectory(minidriver)
add_subdirectory(minidummy)
add_subdirectory(zy1000)

add_library(jtag STATIC
	adapter.c
	commands.c
	core.c
	interface.c
	interfaces.c
	swim.c
	tcl.c)

set_property(TARGET jtag PROPERTY POSITION_INDEPENDENT_CODE ON)
target_link_libraries(jtag drivers)
