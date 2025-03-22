hacl_src = [
	'Hacl_Hash_MD5.c',
	'Hacl_Hash_SHA1.c',
	'Hacl_Hash_SHA2.c',
	'Hacl_Hash_SHA3.c',
	'Hacl_Hash_Blake2b.c',
	'Hacl_Hash_Blake2s.c',

	'Hacl_HMAC.c',
	'Hacl_Streaming_HMAC.c',

	'Lib_Memzero0.c'
]

hacl_include = [
	include_directories('.'),
	include_directories('include')
]

hacl_priv_flags = []
hacl_pub_flags = []

if hacl_can_compile_simd128
	hacl_src += 'Hacl_Hash_Blake2s_Simd128.c'
	hacl_priv_flags += [hacl_simd128_args, '-DHACL_CAN_COMPILE_VEC128']
	hacl_pub_flags += '-D_Py_HACL_CAN_COMPILE_VEC128'
endif
if hacl_can_compile_simd256
	hacl_src += 'Hacl_Hash_Blake2b_Simd256.c'
	hacl_priv_flags += [hacl_simd256_args, '-DHACL_CAN_COMPILE_VEC256']
	hacl_pub_flags += '-D_Py_HACL_CAN_COMPILE_VEC256'
endif

if not have_explicit_bzero
	hacl_priv_flags += '-DLINUX_NO_EXPLICIT_BZERO'
endif

hacl_lib = static_library('hacl', hacl_src,
	c_args: hacl_priv_flags,
	include_directories: hacl_include
)

hacl_dep = declare_dependency(
	compile_args: hacl_pub_flags,
	include_directories: hacl_include,
	link_with: hacl_lib
)
