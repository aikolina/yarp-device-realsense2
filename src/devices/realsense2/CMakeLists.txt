# Copyright (C) 2006-2020 Istituto Italiano di Tecnologia (IIT)
# All rights reserved.
#
# This software may be modified and distributed under the terms of the
# BSD-3-Clause license. See the accompanying LICENSE file for details.

yarp_prepare_plugin(realsense2
  CATEGORY device
  TYPE realsense2Driver
  INCLUDE realsense2Driver.h
  EXTRA_CONFIG WRAPPER=RGBDSensorWrapper
  DEPENDS "realsense2_FOUND"
  DEFAULT ON
)

if(ENABLE_realsense2)
  yarp_add_plugin(yarp_realsense2)

  target_sources(yarp_realsense2
    PRIVATE
      realsense2Driver.cpp
      realsense2Driver.h
  )

  target_link_libraries(yarp_realsense2
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
      realsense2::realsense2
  )

  yarp_install(
    TARGETS yarp_realsense2
    EXPORT yarp-device-realsense2
    COMPONENT yarp-device-realsense2
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set_property(TARGET yarp_realsense2 PROPERTY FOLDER "Plugins/Device")
endif()

yarp_prepare_plugin(realsense2withIMU
  CATEGORY device
  TYPE realsense2withIMUDriver
  INCLUDE realsense2withIMUDriver.h
  EXTRA_CONFIG WRAPPER=RGBDSensorWrapper
  DEPENDS "TARGET YARP::YARP_math;realsense2_FOUND;"
  DEFAULT ON
)

if(ENABLE_realsense2withIMU)
  yarp_add_plugin(yarp_realsense2withIMU)

  target_sources(yarp_realsense2withIMU
    PRIVATE
      realsense2Driver.cpp
      realsense2withIMUDriver.cpp
      realsense2withIMUDriver.h
  )

  target_compile_definitions(yarp_realsense2withIMU
    PRIVATE
      _USE_MATH_DEFINES
  )

  target_link_libraries(yarp_realsense2withIMU
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
      YARP::YARP_math
      realsense2::realsense2
  )

  yarp_install(
    TARGETS yarp_realsense2withIMU
    EXPORT yarp-device-realsense2
    COMPONENT yarp-device-realsense2
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR})

  set(YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS ${YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS} PARENT_SCOPE)

  set_property(TARGET yarp_realsense2withIMU PROPERTY FOLDER "Plugins/Device")
endif()

yarp_prepare_plugin(realsense2Tracking
  CATEGORY device
  TYPE realsense2Tracking
  INCLUDE realsense2Tracking.h
  DEPENDS "TARGET YARP::YARP_math;realsense2_FOUND;"
  DEFAULT ON
)

if(ENABLE_realsense2Tracking)
  yarp_add_plugin(yarp_realsense2Tracking)

  target_sources(yarp_realsense2Tracking
    PRIVATE
      realsense2Tracking.cpp
      realsense2Tracking.h
  )

  target_compile_definitions(yarp_realsense2Tracking
    PRIVATE
      _USE_MATH_DEFINES
  )

  target_link_libraries(yarp_realsense2Tracking
    PRIVATE
      YARP::YARP_os
      YARP::YARP_sig
      YARP::YARP_dev
      YARP::YARP_math
      realsense2::realsense2
  )

  yarp_install(
    TARGETS yarp_realsense2Tracking
    EXPORT yarp-device-realsense2
    COMPONENT yarp-device-realsense2
    LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
    ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
    YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
  )

  set_property(TARGET yarp_realsense2Tracking PROPERTY FOLDER "Plugins/Device")
endif()
