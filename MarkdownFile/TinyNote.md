# TinyNote
1. 验证启动模式，检查 UEFI 位数：
   ```
   # cat /sys/firmware/efi/fw_platform_size
   ```
2. 无线网络连接到互联网
   - 使用 `# ip link` 列出网路接口
   - 使用 `ip link set 'interface' up` 启用网络接口
   - 为了使用 wpa_cli，必须为 wpa_supplicant 指定一个**控制接口**，并且必须授予它**更新配置的权限**。为此，请创建一个最小的配置文件：
     ```
     /etc/wpa_supplicant/wpa_supplicant.conf
     ----
     ctrl_interface=/run/wpa_supplicant
     update_config=1
     ```
    - 使用指定的网络接口和配置文件来连接无线网络:
       ```
       # wpa_supplicant -B -i 'interface' -c /etc/wpa_supplicant/wpa_supplicant.conf
       ```
    - 运行 `# wpa_cli -i 'interface'` 命令，启动一个交互式的命令行界面
    - 使用 `scan` and `scan_results` 命令查看可用的网络：
      ```
      > scan
      OK
      <3>CTRL-EVENT-SCAN-RESULTS
      > scan_results
      bssid / frequency / signal level / flags / ssid
      00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
      11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID
      ```
    - 要关联 `MYSSID`，请添加网络，设置凭据并启用它：
      ```
      > add_network
      0
      > set_network 0 ssid "MYSSID"
      > set_network 0 psk "passphrase"
      > enable_network 0
      <2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]
      ```
    - 如果 SSID 没有密码身份验证，则必须将命令 `set_network 0 psk "passphrase"` 替换为 `set_network 0 key_mgmt NONE`，从而将网络显式配置为无密钥。<br>
      *注意：每个网络都按数字编制索引，因此第一个网络的索引为 0。*
    - 最后将此网络保存在配置文件中并退出wpa_cli：
      ```
      > save_config
      OK
      > quit
      ```
    - 启动指定网络接口的守护程序，请**启动/启用** `# systemctl start/enable dhcpcd@'interface'.service`。
    - dhcpcd 'interface'
  
# timedatectl
# fdisk -l
# fdisk /dev/the_disk_to_be_partitioned
# mkfs.ext4 /dev/root_partition
# mkswap /dev/swap_partition
# mkfs.fat -F 32 /dev/efi_system_partition
# mount /dev/root_partition /mnt
# mount --mkdir /dev/efi_system_partition /mnt/boot
# swapon /dev/swap_partition
# curl https://archlinux.org/mirrorlist/all/ -o /etc/pacman.d/mirrorlist
# pacman -Syu
# pacstrap -K /mnt base linux linux-firmware vim wpa_supplicant dhcpcd intel-ucode
# genfstab -U /mnt >> /mnt/etc/fstab
# arch-chroot /mnt
# ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
# hwclock --systohc
# vim /etc/locale.gen
# locale-gen
vim /etc/locale.conf
LANG=en_US.UTF-8
# echo "ArchLinux" >> /etc/hostname
# echo "127.0.0.1 localhost" >> /etc/hosts
# echo "::1 localhost" >> /etc/hosts
# echo "127.0.1.1 ArchLinux" >> /etc/hosts
# passwd
# pacman -S grub efibootmgr
# mount /dev/sda1 /boot
# grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB
# grub-mkconfig -o /boot/grub/grub.cfg
# ls /boot
# exit 
# reboot
重新配置网络





















