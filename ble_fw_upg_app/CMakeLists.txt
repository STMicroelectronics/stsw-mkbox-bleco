# Copyright (c) 2024 STMicroelectronics
#
# SPDX-License-Identifier: Apache-2.0
#
cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

project(app LANGUAGES C)

target_sources(app PRIVATE src/main.c)
target_sources(app PRIVATE src/ble_fw.c)

set(hal_dir            ${CMAKE_CURRENT_SOURCE_DIR}/..)
set(blob_gen_inc_file  ${ZEPHYR_BINARY_DIR}/include/generated/dtm.bin.inc)

if(CONFIG_BOARD_SENSORTILE_BOX)
  set(hal_blobs_dir      ${hal_dir}/img/steval-mkbox)
elseif(CONFIG_BOARD_SENSORTILE_BOX_PRO)
  set(hal_blobs_dir      ${hal_dir}/img/steval-mkboxpro)
else() # it's not a Sensortile Box board
  set(hal_blobs_dir      "")
endif()

set(blob_hcd_file       ${hal_blobs_dir}/DTM_SPI_WITH_UPDATER_CONTROLLER.bin)

# generate Bluetooth include blob from .bin
if(EXISTS ${blob_hcd_file})
  message(INFO " generate include of ble-fw blob: ${blob_hcd_file}")
  generate_inc_file_for_target(app ${blob_hcd_file} ${blob_gen_inc_file})
endif()
