if (TARGET tinyusb_device)
  add_executable (pio_ir_loopback ir_loopback.c)

  # link the executable using the IR transmit and receive libraries
  #
  target_link_libraries(pio_ir_loopback LINK_PUBLIC
    pico_stdlib
    hardware_pio
    nec_transmit_library
    nec_receive_library
    )

  # enable usb output, disable uart output
  pico_enable_stdio_usb(pio_ir_loopback 1)
  pico_enable_stdio_uart(pio_ir_loopback 0)  

  pico_add_extra_outputs(pio_ir_loopback)

  # add url via pico_set_program_url
  example_auto_set_url(pio_ir_loopback)
elseif(PICO_ON_DEVICE)
    message(WARNING "not building hello_usb because TinyUSB submodule is not initialized in the SDK")
endif()