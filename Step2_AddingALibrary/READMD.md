# Adding a Library (Step 2)

Now we will add a library to our project. This library will contain our own implementation for computing the square root of a number. The executable can then use this library instead of the standard square root function provided by the compiler. For this tutorial we will put the library into a subdirectory called MathFunctions. It will have the following one line CMakeLists.txt file:
	
	add_library(MathFunctions mysqrt.cxx)

The source file mysqrt.cxx has one function called mysqrt that provides similar functionality to the compiler's sqrt function. To make use of the new library we add an add_subdirectory call in the top level CMakeLists.txt file so that the library will get built. We also add another include directory so that the MathFunctions/MathFunctions.h header file can be found for the function prototype. The last change is to add the new library to the executable. The last few lines of the top level CMakeLists.txt file now look like:

	include_directories("${PROJECT_SOURCE_DIR}/MathFunctions")
	add_subdirectory(MathFunctions)
	#
	# add the executable
	add_executable(Tutorial tutorial.cxx)
	target_link_libraries(Tutorial MathFunctions)

Now let us consider making the MathFunctios library optional. In this tutorial there really isn't any reason to do so, but with larger libraries or libraries that rely on third party code you might want to. The first step is to add an option to the top level CMakeLists.txt file.

	# should we use our own math functions?
	option(USE_MYMATH
		"Use tutorial provided math implementation" ON)

This will show up in the CMake GUI with a default value of ON that the user can change as desired. This setting will be stored in the cache so that the user does not need to keep setting it each time they run CMake on this project. The enxt change is to make the build and linking of the MathFunctions library conditional. 