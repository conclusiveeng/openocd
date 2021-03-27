include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	${CMAKE_CURRENT_SOURCE_DIR}/helper
	${CMAKE_CURRENT_SOURCE_DIR}/../jimtcl
	${CMAKE_CURRENT_BINARY_DIR}/../jimtcl-cmake
	${CMAKE_CURRENT_BINARY_DIR})

add_subdirectory(flash)
add_subdirectory(helper)
add_subdirectory(jtag)
add_subdirectory(pld)
add_subdirectory(rtos)
add_subdirectory(server)
add_subdirectory(svf)
add_subdirectory(target)
add_subdirectory(transport)
add_subdirectory(xsvf)

set(STARTUP_TCL_FILES
	${CMAKE_CURRENT_SOURCE_DIR}/helper/startup.tcl
	${CMAKE_CURRENT_SOURCE_DIR}/jtag/startup.tcl
	${CMAKE_CURRENT_SOURCE_DIR}/target/startup.tcl
	${CMAKE_CURRENT_SOURCE_DIR}/flash/startup.tcl
	${CMAKE_CURRENT_SOURCE_DIR}/server/startup.tcl)

add_custom_command(
	OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl
	COMMAND cat
	ARGS ${STARTUP_TCL_FILES} > ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl
	MAIN_DEPENDENCY helper/startup.tcl
	VERBATIM)

add_custom_command(
	OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/startup_tcl.inc
	COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/helper/bin2char.sh
	ARGS < ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl > ${CMAKE_CURRENT_BINARY_DIR}/startup_tcl.inc
	MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl
	VERBATIM)

add_library(libopenocd SHARED
	openocd.c
	hello.c
	${CMAKE_CURRENT_BINARY_DIR}/startup_tcl.inc)

add_definitions(-DPKGBLDDATE="" -DRELSTR="" -DGITVERSION="")
add_definitions(-DLIBUSB1COMMIT="")
target_link_libraries(libopenocd dl jim flash helper jtag pld rtos server svf target transport xsvf)

add_executable(openocd main.c)
target_link_libraries(openocd libopenocd)
