#### Project ####
project('comptonmod', 'c',
        version: '0.1.1',
        meson_version: '>= 0.58.0')

add_project_arguments('-D__UNUSED__=__attribute__((unused))', language: 'c')

gettext_domain = 'e-module-' + meson.project_name()

#### Enlightenment ####
dep_e = dependency('enlightenment')
e_modules_dir = dep_e.get_variable('modules')
e_module_arch = dep_e.get_variable('module_arch')

#### Install dirs ####
mod_install_dir = join_paths(e_modules_dir, meson.project_name())
lib_install_dir = join_paths(mod_install_dir, e_module_arch)
config_install_dir = '/etc'

#### config.h ####
config_h = configuration_data()
config_h.set_quoted('PACKAGE', meson.project_name())
config_h.set('__UNUSED__', '__attribute__((unused))')
config_dir = include_directories('.')

#### Edje cc ####
edje_cc = get_option('edje-cc')
if edje_cc == ''
edje_cc = find_program('edje_cc')
endif

picom = find_program('picom')

#### module sources ####
subdir('src')
subdir('data')

#### write config file ####
configure_file(output: 'config.h', configuration: config_h)

#### module.desktop ####
install_data('module.desktop',
  install_dir : mod_install_dir
)

#### Report ####
if meson.version().version_compare('>=0.53')
   summary({'install': lib_install_dir,
           }, section: 'Directories')
endif
