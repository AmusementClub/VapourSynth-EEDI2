project('EEDI2', 'cpp',
  default_options : ['buildtype=release', 'b_ndebug=if-release', 'cpp_std=c++14'],
  meson_version : '>=0.51.0',
  version : '7'
)

cxx = meson.get_compiler('cpp')
gcc_syntax = cxx.get_argument_syntax() == 'gcc'

sources = 'EEDI2/EEDI2.cpp'

if gcc_syntax
  vapoursynth_dep = dependency('vapoursynth').partial_dependency(compile_args : true, includes : true)
  install_dir = vapoursynth_dep.get_variable(pkgconfig: 'libdir') / 'vapoursynth'

  add_project_arguments('-ffast-math', language : 'cpp')

  if host_machine.cpu_family().startswith('x86')
    add_project_arguments('-mfpmath=sse', '-msse2', language : 'cpp')
  endif
else
  vapoursynth_dep = []
  install_dir = get_option('libdir') / 'vapoursynth'
endif

shared_module('eedi2', sources,
  dependencies : vapoursynth_dep,
  install : true,
  install_dir : install_dir,
  gnu_symbol_visibility : 'hidden'
)
