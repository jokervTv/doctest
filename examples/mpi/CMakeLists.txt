find_package(MPI COMPONENTS CXX)
if(MPI_FOUND)
    add_executable(test_mpi main.cpp)
    target_link_libraries(test_mpi doctest ${CMAKE_THREAD_LIBS_INIT} MPI::MPI_CXX)
    add_executable(test_mpi_with_main mpi.cpp)
    target_link_libraries(test_mpi_with_main doctest ${CMAKE_THREAD_LIBS_INIT} MPI::MPI_CXX)

    doctest_add_test(NO_OUTPUT NAME test_mpi           COMMAND mpirun -np 3 $<TARGET_FILE:test_mpi>)
    doctest_add_test(NO_OUTPUT NAME test_mpi_with_main COMMAND mpirun -np 3 $<TARGET_FILE:test_mpi_with_main>)
endif()
