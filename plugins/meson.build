# plugins/meson.build
# Generate GNOME Settings Daemon plugin autostart desktop files for Slackware

# List all GNOME Settings Daemon plugin components
gsd_plugins = [
  'A11ySettings',
  'Color',
  'Datetime',
  'Housekeeping',
  'Keyboard',
  'MediaKeys',
  'Power',
  'PrintNotifications',
  'Rfkill',
  'ScreensaverProxy',
  'Sharing',
  'Smartcard',
  'Sound',
  'UsbProtection',
  'Wwan',
  'XSettings',
]

# Install directory for autostart files
autostart_dir = join_paths(get_option('sysconfdir'), 'xdg', 'autostart')

# For each plugin, generate a .desktop file using configure_file()
foreach plugin : gsd_plugins
  desktop_in = 'org.gnome.SettingsDaemon.Real.desktop.in'
  desktop_out = 'org.gnome.SettingsDaemon.@0@.desktop'.format(plugin)

  # Configure substitutions
  configure_file(
    input: desktop_in,
    output: desktop_out,
    configuration: {
      'pluginname': plugin,
      'description': 'GNOME Settings Daemon {} plugin'.format(plugin),
      'libexecdir': join_paths(get_option('prefix'), get_option('libexecdir')),
      # Slackware does not use systemd, so we set this to false
      'systemd_hidden': 'false',
    },
    install: true,
    install_dir: autostart_dir,
  )
endforeach

# Also install a dummy desktop file for completeness
configure_file(
  input: 'org.gnome.SettingsDaemon.Dummy.desktop.in',
  output: 'org.gnome.SettingsDaemon.Dummy.desktop',
  configuration: {
    'pluginname': 'dummy',
  },
  install: true,
  install_dir: autostart_dir,
)
