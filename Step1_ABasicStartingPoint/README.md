# A Basic Starting Point (Step1)

The most basic project is an executable built from source code files. For simple projects a two line CMakeLists.txt file is all that is required. This will be the starting point for our tutorial. The CMakeLists.txt file looks like:

	cmake_minimum_required(VERSION 2.6)
	project(Tutorial)
	add_executable(Tutorial tutorial.cxx)



