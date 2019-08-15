project('dxvk-nvapi', ['c'], version : '4.11', meson_version : '>= 0.49')

add_project_arguments('-D__WINESRC__', language : ['c'])

if target_machine.cpu_family() == 'x86_64'
  target_arch  = '-m64'
  nvapi_bits   = '64'
else
  target_arch  = '-m32'
  nvapi_bits   = ''
endif

idl_generator = generator(find_program('widl'),
  output    : [ '@BASENAME@.h' ],
  arguments : [ target_arch, '-o', '@OUTPUT@', '-D__WINESRC__', '@EXTRA_ARGS@', '@INPUT@' ])


nvapi_src  = ['nvapi.c', idl_generator.process('dxvk.idl')]

nvapi_dll  = 'nvapi@0@.dll'  .format(nvapi_bits)
nvapi_spec = 'nvapi@0@.spec' .format(nvapi_bits)

shared_library(nvapi_dll, nvapi_src,
  name_prefix         : '',
  dependencies        : declare_dependency(link_args: [ '-ld3d11' ]),
  objects             : nvapi_spec,
  install             : true)
