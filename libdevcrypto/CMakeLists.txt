aux_source_directory(. SRC_LIST)

set(EXECUTABLE devcrypto)

file(GLOB HEADERS "*.h")
add_library(${EXECUTABLE} ${SRC_LIST} ${HEADERS})

eth_use(${EXECUTABLE} REQUIRED Dev::devcore Utils::scrypt Cryptopp)

if ((NOT EMSCRIPTEN) AND (NOT DEFINED MSVC))
	eth_use(${EXECUTABLE} REQUIRED Utils::secp256k1)
endif ()

install( TARGETS ${EXECUTABLE} RUNTIME DESTINATION bin ARCHIVE DESTINATION lib LIBRARY DESTINATION lib )
install( FILES ${HEADERS} DESTINATION include/${EXECUTABLE} )

