cmake_minimum_required (VERSION 3.19 FATAL_ERROR)

find_package(cetmodules)

project(mu2e-trig-config VERSION 7.00.00)

include(CetCMakeEnv)
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
cet_cmake_env()
cet_cmake_config()

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/..)

#add_subdirectory(core)
#add_subdirectory(python)
#add_subdirectory(data)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigDigiInputsEpilog.fcl       ${CURRENT_BINARY_DIR} core/trigDigiInputsEpilog.fcl               COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigFilters.fcl                ${CURRENT_BINARY_DIR} core/trigFilters.fcl                        COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigProducers.fcl              ${CURRENT_BINARY_DIR} core/trigProducers.fcl                      COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigRecoSequences.fcl          ${CURRENT_BINARY_DIR} core/trigRecoSequences.fcl                  COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigSequences.fcl              ${CURRENT_BINARY_DIR} core/trigSequences.fcl                      COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/core/trigServices.fcl               ${CURRENT_BINARY_DIR} core/trigServices.fcl                       COPYONLY)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/python/generateMenuFromJSON.py      ${CURRENT_BINARY_DIR} python/generateMenuFromJSON.py              COPYONLY)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/data/physMenu.json                  ${CURRENT_BINARY_DIR} data/physMenu.json                          COPYONLY)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/data/extrPosMenu.json               ${CURRENT_BINARY_DIR} data/extrPosMenu.json                       COPYONLY)

install_fhicl(SUBDIRS core SUBDIRNAME mu2e-trig-config/core)
install_fhicl(SUBDIRS core/producers SUBDIRNAME mu2e-trig-config/core/producers)
install_fhicl(SUBDIRS core/filters   SUBDIRNAME mu2e-trig-config/core/filters)

install(DIRECTORY data DESTINATION ${CMAKE_INSTALL_DATAROOTDIR})
install(DIRECTORY python DESTINATION .)

cet_script(python/generateMenuFromJSON.py)
