```bash

apt insrtall xrdp

usermod -a -G xrdp user

# echo exec /usr/libexec/gnome-flashback-metacity > ~/.xsession

cat << EOF >>  /etc/xrdp/startwm.sh
#!/bin/sh
# xrdp X session start script (c) 2015, 2017, 2021 mirabilos
# published under The MirOS Licence

# Rely on /etc/pam.d/xrdp-sesman using pam_env to load both
# /etc/environment and /etc/default/locale to initialise the
# locale and the user environment properly.

if test -r /etc/profile; then
        . /etc/profile
fi

export STARTUP=/usr/libexec/gnome-flashback-metacity

test -x /etc/X11/Xsession && exec /etc/X11/Xsession
exec /bin/sh /etc/X11/Xsession
EOF


cat << EOF >> /etc/xrdp/xrdp_keyboard.ini

[rdp_keyboard_ru]
keyboard_type=4
keyboard_subtype=1
model=pc104
options=grp:alt_shift_toggle
rdp_layouts=default_rdp_layouts
layouts_map=layouts_map_ru

[layouts_map_ru]
rdp_layout_us=us,ru
rdp_layout_ru=us,ru

EOF

```
