# plugins/meson.build
# Generate GNOME Settings Daemon plugin autostart desktop files dynamically

# Ensure gsd_components is available from the parent scope
# (declared in the top-level meson.build)
assert(defined('gsd_components'), 'gsd_components must be defined in the parent Meson file.')

# Install directory for autostart entries
autostart_dir = join_paths(get_option('sysconfdir'), 'xdg', 'autostart')

# Generate a .desktop file for each GNOME Settings Daemon component
foreach component : gsd_components
  # Extract only the plugin name (the part after the last dot)
  plugin_name = component.split('.')[-1]
  desktop_in = 'org.gnome.SettingsDaemon.Real.desktop.in'
  desktop_out = 'org.gnome.SettingsDaemon.@0@.desktop'.format(plugin_name)

  configure_file(
    input: desktop_in,
    output: desktop_out,
    configuration: {
      'pluginname': plugin_name,
      'description': 'GNOME Settings Daemon {} plugin'.format(plugin_name),
      'libexecdir': join_paths(get_option('prefix'), get_option('libexecdir')),
      'systemd_hidden': 'false',  # Slackware-friendly, no systemd
    },
    install: true,
    install_dir: autostart_dir,
  )
endforeach

# Also install a dummy placeholder autostart entry
configure_file(
  input: 'org.gnome.SettingsDaemon.Dummy.desktop.in',
  output: 'org.gnome.SettingsDaemon.Dummy.desktop',
  configuration: {
    'pluginname': 'dummy',
  },
  install: true,
  install_dir: autostart_dir,
)
