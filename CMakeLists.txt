zephyr_library()

# Only build the behavior on the central, and only when battery reporting is
# actually compiled in (it defines zmk_battery_state_of_charge()). Builds like
# the settings_reset shield disable BLE, which turns battery reporting off; the
# keymap still references &bapp there, but leaving the behavior uncompiled is
# fine (same as the peripheral build) and avoids an undefined-symbol link error.
if (((NOT CONFIG_ZMK_SPLIT) OR CONFIG_ZMK_SPLIT_ROLE_CENTRAL) AND CONFIG_ZMK_BATTERY_REPORTING)
  zephyr_library_sources_ifdef(CONFIG_ZMK_BEHAVIOR_BATT_PCT_PRINTER src/behavior_battery_percentage_printer.c)
  zephyr_include_directories(${APPLICATION_SOURCE_DIR}/include)
endif()
