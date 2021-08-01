service provision_keys /vendor/bin/init.provision_keys.sh
class core
user system
group system
disabled
oneshot

on property:persist.vendor.act.mode=1
start provision_keys