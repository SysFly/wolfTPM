if(CONFIG_WOLFTPM)
  zephyr_interface_library_named(wolfTPM)

    zephyr_include_directories(
      ${APPLICATION_CONFIG_DIR}
      ${APPLICATION_CONFIG_DIR}/src
    )

    zephyr_include_directories(
        ${ZEPHYR_CURRENT_MODULE_DIR}
        ${ZEPHYR_CURRENT_MODULE_DIR}/wolftpm
        ${ZEPHYR_CURRENT_MODULE_DIR}/zephyr
    )

    zephyr_library()
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/zephyr/zephyr_init.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_asn.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_cryptocb.c)
    # zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_linux.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_packet.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_param_enc.c)
    # zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_swtpm.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_tis.c)
    # zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_winapi.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2_wrap.c)
    zephyr_library_sources(${ZEPHYR_CURRENT_MODULE_DIR}/src/tpm2.c)

    add_compile_definitions(wolfTPM INTERFACE 
      WOLFSSL_USER_SETTINGS
      WOLFSSL_ZEPHYR
      WOLFTPM2_NO_HEAP
      WOLFTPM_NO_LOCK
      WOLFTPM2_NO_WOLFCRYPT
    )
    target_include_directories(wolfTPM INTERFACE
      ${ZEPHYR_CURRENT_MODULE_DIR}/
      ${ZEPHYR_CURRENT_MODULE_DIR}/wolftpm
      ${ZEPHYR_CURRENT_MODULE_DIR}/zephyr
    )

    target_link_libraries(wolfTPM INTERFACE zephyr_interface wolfSSL)
endif()
