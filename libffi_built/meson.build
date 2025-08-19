project('libffi-prebuilt', 'c',
  version: '3.4.5',
)

# Path to your prebuilt library inside this subproject
prebuilt_lib_path = meson.current_source_dir() / 'lib' / 'libffi.a'

# Create a Meson target from the prebuilt library
libffi_a = custom_target(
  'libffi-a',
  output: 'libffi.a',
  input: prebuilt_lib_path,
  command: ['cp', '@INPUT@', '@OUTPUT@'],
  build_by_default: true,
  install: true,
  install_dir: get_option('libdir')
)

# Include directory for headers
inc_dir = include_directories('include')

# Install headers
install_headers(
  'include/ffi.h',
  'include/ffitarget.h',
)

# Declare the dependency so that GLib's meson.build can use it
libffi_dep = declare_dependency(
  link_with: libffi_a,
  include_directories: inc_dir
)

# Override the dependency name so Meson resolves "libffi" to this
meson.override_dependency('libffi', libffi_dep)

