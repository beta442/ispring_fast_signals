file(GLOB LIBFASTSIGNALS_SRC "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/include/*.h")

set(FASTSIGNALS_LIB_NAME libfastsignals)

add_library(${FASTSIGNALS_LIB_NAME} ${LIBFASTSIGNALS_SRC})

custom_enable_cxx17(${FASTSIGNALS_LIB_NAME})

target_include_directories(${FASTSIGNALS_LIB_NAME} INTERFACE "${CMAKE_SOURCE_DIR}")

if(MSVC)

get_filename_component(TOP_LEVEL_DIR ../ ABSOLUTE)

set_target_properties(
	${FASTSIGNALS_LIB_NAME}
PROPERTIES
	VS_USER_PROPS "${TOP_LEVEL_DIR}/libfastsignals_build_options.props"
	OUTPUT_NAME "libfastsignals$(DebugSuffixOpt)-$(PlatformToolset)$(PlatformSuffix)"
)

endif()
