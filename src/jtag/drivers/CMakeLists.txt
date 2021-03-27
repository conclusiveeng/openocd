add_library(drivers STATIC
	driver.c
	jtag_usb_common.c
	libusb_helper.c
	ftdi.c
	mpsse.c)

set_property(TARGET drivers PROPERTY POSITION_INDEPENDENT_CODE ON)
target_link_libraries(drivers PUBLIC ${LIBUSB_LIBRARIES})
