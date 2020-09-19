## Assets Target Configuration ##

# MD5 generation
set(SRB2_ASSET_ALL
	${CMAKE_CURRENT_SOURCE_DIR}/srb2.srb
	${CMAKE_CURRENT_SOURCE_DIR}/zones.td
	${CMAKE_CURRENT_SOURCE_DIR}/player.td
	${CMAKE_CURRENT_SOURCE_DIR}/rings.dta
	${CMAKE_CURRENT_SOURCE_DIR}/assetpack.td
	${CMAKE_CURRENT_SOURCE_DIR}/tddata.td
	${CMAKE_CURRENT_SOURCE_DIR}/music.dta
	${CMAKE_CURRENT_SOURCE_DIR}/music.td
)

set(SRB2_ASSET_HASHED
	srb2.srb
	zones.td
	player.td
	rings.dta
	assetpack.td
	tddata.td
)

foreach(SRB2_ASSET ${SRB2_ASSET_HASHED})
	file(MD5 ${CMAKE_CURRENT_SOURCE_DIR}/${SRB2_ASSET} "SRB2_ASSET_${SRB2_ASSET}_HASH")
	set(SRB2_ASSET_${SRB2_ASSET}_HASH ${SRB2_ASSET_${SRB2_ASSET}_HASH} PARENT_SCOPE)
endforeach()

# Installation

if(CLANG)
	get_target_property(outname SRB2SDL2 OUTPUT_NAME)
	install(FILES ${SRB2_ASSET_ALL}
		DESTINATION "${outname}.app/Contents/Resources"
	)
else()
	install(FILES ${SRB2_ASSET_ALL}
		DESTINATION .
	)
endif()
