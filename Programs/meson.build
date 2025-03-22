python_bin = executable('python', 'python.c',
	dependencies: libpython_dep,
	install: true
)

configure_file(
	configuration: build_pth,
	input: 'build._pth.in',
	output: fs.name(python_bin.full_path()) + '._pth'
)
