cmake_minimum_required(VERSION 3.0)
project(tinyfsm_examples)

set(COMPILE_FLAGS "-std=c++11 -fno-exceptions -fno-rtti  -pedantic -Os")


# not msvc
if(NOT MSVC)
    set(COMPILE_FLAGS "${COMPILE_FLAGS} -Wall -Wextra -Wctor-dtor-privacy -Wcast-align -Wpointer-arith -Wredundant-decls -Wshadow -Wcast-qual -Wcast-align")
endif()

# processing each example

# elevator example
file(GLOB EXAMPLES_ELEVATOR_CPPS examples/elevator/*.cpp)
file(GLOB EXAMPLES_ELEVATOR_HEADERS examples/elevator/*.cpp)

add_executable(
    elevator
    ${EXAMPLES_ELEVATOR_HEADERS}
    ${EXAMPLES_ELEVATOR_CPPS})

target_include_directories(
    elevator PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/include
    ${CMAKE_CURRENT_LIST_DIR}/examples/elevator
)
target_compile_options(elevator PRIVATE ${COMPILE_FLAGS})

# api examples
file(GLOB EXAMPLES_API_CPPS examples/api/*.cpp)
foreach(EXAMPLE_API_CPP ${EXAMPLES_API_CPPS})
    get_filename_component(EXAMPLE_API_NAME ${EXAMPLE_API_CPP} NAME_WE)
    add_executable(${EXAMPLE_API_NAME} ${EXAMPLE_API_CPP})
    target_include_directories(
        ${EXAMPLE_API_NAME} PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}/include
    )
    target_compile_options(${EXAMPLE_API_NAME} PRIVATE ${COMPILE_FLAGS})
endforeach()



