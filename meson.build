project('zlib', 'c',
        version : '1.2.11',
        license : 'zlib',
  meson_version : '>= 0.48.0'
)

cc = meson.get_compiler('c')

link_args = []
compile_args = []

if cc.get_id() == 'msvc'
  add_project_arguments('-D_CRT_SECURE_NO_DEPRECATE',
    '-D_CRT_NONSTDC_NO_DEPRECATE', language : 'c')
else
  # Don't spam consumers of this wrap with these warnings
  compile_args += cc.get_supported_arguments(['-Wno-implicit-fallthrough',
                                              '-Wno-implicit-function-declaration'])
  if cc.get_id() == 'gcc' and host_machine.system() != 'windows'
    vflag = '-Wl,--version-script,@0@/zlib.map'.format(meson.current_source_dir())
    link_args += [vflag]
  endif
endif

src = files(
  'adler32.c',
  'crc32.c',
  'deflate.c',
  'infback.c',
  'inffast.c',
  'inflate.c',
  'inftrees.c',
  'trees.c',
  'zutil.c',
  'compress.c',
  'uncompr.c',
  'gzclose.c',
  'gzlib.c',
  'gzread.c',
  'gzwrite.c'
)

zlib = static_library('z', src,
     c_args : compile_args,
  link_args : link_args,
    install : false
)

incdir = include_directories('.')

zlib_dep = declare_dependency(
  include_directories : incdir,
            link_with : zlib,
              version : meson.project_version()
)
