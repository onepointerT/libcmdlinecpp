
include_directories( . )

file( GLOB LIBCMDLINECPP_HEADERS *.hpp )

set( LIBCMDLINECPP_SOURCE actions.cpp
                          arguments.cpp
                          cmdline.cpp
                          exceptions.cpp
                          parameters.cpp )

if ( BUILD_WITH_LOGIO_FUNCTIONALITY )
	set( LIBCMDLINECPP_SOURCE ${LIBCMDLINECPP_SOURCE} cmdlinelogio.cpp )
endif()


if ( BUILD_WITH_CONFIG_FUNCTIONALITY )
	set( LIBCMDLINECPP_SOURCE ${LIBCMDLINECPP_SOURCE} cmdlineconfig.cpp configpreset.cpp )
endif()


if( CMDLINECPP_SHARED )
	add_library( cmdlinecpp SHARED ${LIBCMDLINECPP_SOURCE} )
	set( CMDLINECPP_PKGCONFIG_LIBNAME "libcmdlinecpp.so" )
else()
	add_library( cmdlinecpp STATIC ${LIBCMDLINECPP_SOURCE} )
	set( CMDLINECPP_PKGCONFIG_LIBNAME "libcmdlinecpp.a" )
endif()


add_subdirectory( examples )


if( CMDLINECPP_INSTALL_LIBS )
	install(TARGETS cmdlinecpp DESTINATION ${CMDLINECPP_LIB_INSTALL_DIR} )
	install(FILES ${LIBCMDLINECPP_HEADERS} DESTINATION ${CMDLINECPP_HEADER_INSTALL_DIR} )
endif()


