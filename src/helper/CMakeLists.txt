add_library(helper STATIC
	binarybuffer.c
	command.c
	configuration.c
	fileio.c
	ioutil.c
	ioutil_stubs.c
	jep106.c
	jim-nvp.c
	log.c
	options.c
	replacements.c
	time_support.c
	time_support_common.c
	util.c)

set_property(TARGET helper PROPERTY POSITION_INDEPENDENT_CODE ON)
