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

add_custom_command(
	OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl
	COMMAND sh
	ARGS -c "cat ${CMAKE_CURRENT_SOURCE_DIR}/helper/startup.tcl ${CMAKE_CURRENT_SOURCE_DIR}/jtag/startup.tcl ${CMAKE_CURRENT_SOURCE_DIR}/target/startup.tcl ${CMAKE_CURRENT_SOURCE_DIR}/flash/startup.tcl ${CMAKE_CURRENT_SOURCE_DIR}/server/startup.tcl > ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl" MAIN_DEPENDENCY helper/startup.tcl)

add_custom_command(
	OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/startup_tcl.inc
	COMMAND sh
	ARGS -c "${CMAKE_CURRENT_SOURCE_DIR}/helper/bin2char.sh < ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl > ${CMAKE_CURRENT_BINARY_DIR}/startup_tcl.inc" MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/startup.tcl)

add_library(openocd SHARED openocd.c)
add_definitions(openocd -DPKGBLDDATE="" -DRELSTR="" -DGITVERSION="")
add_definitions(openocd -DLIBUSB1COMMIT="")
target_link_libraries(openocd flash helper jtag pld rtos server svf target transport xsvf)
