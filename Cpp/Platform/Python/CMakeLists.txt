FILE(GLOB Header "*.h")

SET(PythonSrc 
	${Header}
	PythonInit.cc 
	PythonInterpreter.cc
)

ADD_LIBRARY(PythonInterpreter ${PythonSrc})
SET_PROPERTY(TARGET PythonInterpreter PROPERTY FOLDER "Platform/Python")

ADD_EXECUTABLE(PythonInitTest PythonInitTest.cc)
ADD_EXECUTABLE(PythonInterpreterTest PythonInterpreterTest.cc)

SET(Tests 
	PythonInitTest 
	PythonInterpreterTest
)

FOREACH(Test ${Tests})
	TARGET_LINK_LIBRARIES(${Excute}
		PythonInterpreter
		${ThirdPartyLibs}
	)
	ADD_TEST(${Test} ${Test})
	SET_PROPERTY(TARGET ${Test} PROPERTY FOLDER "Tests/Platform/Python")
ENDFOREACH()