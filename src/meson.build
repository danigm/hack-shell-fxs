gnome_shell_deps = [
  clutter_dep,
  cogl_dep,
  mutter_dep,
]

gnome_shell_cflags = [
  '-DCLUTTER_ENABLE_EXPERIMENTAL_API',
  '-DCOGL_ENABLE_EXPERIMENTAL_API',
  '-DVERSION="@0@"'.format(meson.project_version()),
  '-DDATADIR="@0@"'.format(datadir),
]

libshell_public_headers = [
  'shell-code-view-effect.h',
]

libshell_private_headers = [
]

libshell_private_sources = [
]

libshell_sources = [
  'shell-code-view-effect.c',
]

libshell_enums = gnome.mkenums_simple('shell-enum-types',
  sources: libshell_public_headers
)

libshell_gir_sources = [
  libshell_enums,
  libshell_public_headers,
  libshell_sources
]

libshell_no_gir_sources = [
  libshell_private_headers,
  libshell_private_sources
]

libshell = library('gnome-shell',
  sources: libshell_gir_sources + libshell_no_gir_sources,
  dependencies: gnome_shell_deps,
  c_args: gnome_shell_cflags,
  build_rpath: mutter_typelibdir,
  install_dir: pkglibdir,
  install: true
)

libshell_dep = declare_dependency(link_with: libshell)

libshell_gir_includes = [
  'Clutter-@0@'.format(mutter_api_version),
  'ClutterX11-@0@'.format(mutter_api_version),
  'Meta-@0@'.format(mutter_api_version),
]

gnome.generate_gir(libshell,
  sources: libshell_gir_sources,
  nsversion: '0.1',
  namespace: 'Shell',
  includes: libshell_gir_includes,
  extra_args: ['--quiet'],
  install: true
)
