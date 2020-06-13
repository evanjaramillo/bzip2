CMAKE_MINIMUM_REQUIRED( VERSION 3.0 )

PROJECT( bzip2 LANGUAGES C)

SET( CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH} )

INCLUDE( RemoveCompileOption )

ADD_LIBRARY( bzip2 SHARED
	src/blocksort.c
	src/huffman.c
	src/crctable.c
	src/randtable.c
	src/bzlib.c
	src/decompress.c
	src/compress.c
	#src/bzip2.c
	#src/bzip2recover.c
	#src/dlltest.c
	#src/mk251.c
	#src/spewG.c
	#src/unzcrash.c    	       
)

TARGET_INCLUDE_DIRECTORIES( bzip2

	PUBLIC
		$<INSTALL_INTERFACE:include>
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
	PRIVATE
	 	${CMAKE_CURRENT_SOURCE_DIR}/src
		${CMAKE_CURRENT_SOURCE_DIR}/include/priv
		
)

TARGET_COMPILE_OPTIONS( bzip2
       
	PRIVATE
		-fpic -fPIC -Wall -Winline -O2 -g

)

IF( WIN32 )

	RemoveCompileOption( "/RTC1" )

ENDIF( )
