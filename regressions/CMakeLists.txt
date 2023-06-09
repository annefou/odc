
list( APPEND regressions_data_files
    odb_387_mdset.odb
    odb_463.odb
    sd_45315-reduced.odb
    sd_45479_source.odb
    sd_45479_compare.odb
)

ecbuild_get_test_multidata( TARGET odc_get_regressions_data
                            #DIRNAME odc/tests
                            NAMES ${regressions_data_files}
                            NOCHECK )

set(regressions_scripts

    ODB-374.sh
    ODB-387-and-388.sh
    ODB-463.sh
    SD-45315.sh
    SD-45479.sh
    ODB-529.sh
)

foreach( _script ${regressions_scripts})
    ecbuild_add_test(
        TYPE script
        COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/${_script}
        ENVIRONMENT PATH=${CMAKE_BINARY_DIR}/bin:$ENV{PATH}
        TEST_DEPENDS odc_get_test_data odc_get_regressions_data
    )
endforeach()


# Add a custom target to make these files visible in qtcreator

add_custom_target(
    regressions_file_visibility
    SOURCES ${regressions_scripts}
)
