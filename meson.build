project('hack-shell-fxs', 'c',
  version: '3.36.0',
  meson_version: '>= 0.47.0',
  license: 'GPLv2+'
)

split_version = meson.project_version().split('.')

# We depend on a specific version of the libmutter API. The mutter variants of
# the Cogl and Clutter libraries also use this API version.
# The API version is increased automatically each development cycle,
# starting with 0 in 3.23.x
api_version = (split_version[1].to_int() - 23) / 2
mutter_api_version = '@0@'.format(api_version)

clutter_pc = 'mutter-clutter-' + mutter_api_version
cogl_pc = 'mutter-cogl-' + mutter_api_version
libmutter_pc = 'libmutter-' + mutter_api_version

mutter_req = '>= 3.36.0'

gnome = import('gnome')
i18n  = import('i18n')

prefix = get_option('prefix')

bindir = join_paths(prefix, get_option('bindir'))
datadir = join_paths(prefix, get_option('datadir'))
libdir = join_paths(prefix, get_option('libdir'))
libexecdir = join_paths(prefix, get_option('libexecdir'))
sysconfdir = join_paths(prefix, get_option('sysconfdir'))

pkgdatadir = join_paths(datadir, meson.project_name())
pkglibdir = join_paths(libdir, meson.project_name())

mutter_dep = dependency(libmutter_pc, version: mutter_req)
clutter_dep = dependency(clutter_pc, version: mutter_req)
cogl_dep = dependency(cogl_pc, version: mutter_req)

mutter_typelibdir = mutter_dep.get_pkgconfig_variable('typelibdir')

cc = meson.get_compiler('c')

# Endless-specific: Custom animations
libanimation_glib_dep = dependency('libanimation-glib-0')
libeos_shell_fx_deps = [clutter_dep, libanimation_glib_dep]

subdir('src')
