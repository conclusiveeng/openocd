add_subdirectory(nand)
add_subdirectory(nor)
add_library(flash common.c)
target_link_libraries(flash flash_nand flash_nor)
