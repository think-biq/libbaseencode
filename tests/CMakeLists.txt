
IF(BUILD_TESTING)
    add_executable (test_all
        ../src/base32.c
        ../src/base64.c 
        test-*.c)
    target_link_libraries (test_all -lcriterion)
    add_test (NAME TestAll COMMAND test_all)
ENDIF(BUILD_TESTING)
