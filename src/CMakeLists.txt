add_executable(main main.cpp)

qt5_use_modules(main
	Core
	Widgets)

install(TARGETS main
	DESTINATION bin)
