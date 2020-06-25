hackfx_deps = [
  clutter_dep,
  cogl_dep,
  mutter_dep,
]

hackfx_cflags = [
  '-DCLUTTER_ENABLE_EXPERIMENTAL_API',
  '-DCOGL_ENABLE_EXPERIMENTAL_API',
  '-DVERSION="@0@"'.format(meson.project_version()),
  '-DDATADIR="@0@"'.format(datadir),
]

libhackfx_public_headers = [
  'hackfx-code-view-effect.h',
]

libhackfx_private_headers = [
]

libhackfx_private_sources = [
]

libhackfx_sources = [
  'hackfx-code-view-effect.c',
]

libhackfx_enums = gnome.mkenums_simple('hackfx-enum-types',
  sources: libhackfx_public_headers
)

libhackfx_gir_sources = [
  libhackfx_enums,
  libhackfx_public_headers,
  libhackfx_sources
]

libhackfx_no_gir_sources = [
  libhackfx_private_headers,
  libhackfx_private_sources
]

libhackfx = shared_library('hackfx',
  sources: libhackfx_gir_sources + libhackfx_no_gir_sources,
  dependencies: hackfx_deps,
  c_args: hackfx_cflags,
  install: true
)

libhackfx_dep = declare_dependency(link_with: libhackfx)

libhackfx_gir_includes = [
  'Clutter-@0@'.format(mutter_api_version),
  'ClutterX11-@0@'.format(mutter_api_version),
  'Meta-@0@'.format(mutter_api_version),
]

gnome.generate_gir(libhackfx,
  sources: libhackfx_gir_sources,
  nsversion: '0.1',
  namespace: 'Hackfx',
  includes: libhackfx_gir_includes,
  extra_args: ['--quiet'],
  install: true
)
