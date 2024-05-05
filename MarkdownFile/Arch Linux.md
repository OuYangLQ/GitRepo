# Arch Linux Installation Guide
## 预安装

## 开始安装

### 1. 启动实时环境
*注意：Arch Linux 安装映像不支持**安全启动**。您需要**禁用安全启动**才能启动安装介质。如果需要，可以在完成安装后**设置安全启动**。* 
1. 将当前引导设备指向具有 Arch Linux 安装介质的启动设备。通常，它是通过在**开机自检**阶段按一个键来实现的，如初始屏幕上所示。有关详细信息，请参阅**主板**的手册。
2. 当安装介质的引导加载程序菜单出现时，如果您使用的是 ISO，请选择 Arch Linux 安装介质，然后按 `Enter` 进入安装环境。<br>
- *提示：ISO 使用 systemd-boot 进行 UEFI 引导，使用 syslinux 进行 BIOS 引导。分别使用 `e` 或 `tab` 输入引导参数。*
3. 您将以 root 用户身份登录第一个虚拟控制台，并显示 Zsh shell 提示符。
### 2. 设置控制台键盘布局和字体
略

### 3. 验证启动模式
若要验证启动模式，请检查 UEFI 位数：
```
# cat /sys/firmware/efi/fw_platform_size
```
如果命令返回 `64` ，则系统以 UEFI 模式启动，并具有 64 位 x64 UEFI。如果命令返回 `32`，则系统以 UEFI 模式启动，并具有 32 位 IA32 UEFI;虽然支持此功能，但它会将引导加载程序的选择限制为 systemd-boot 和 GRUB。如果文件不存在，系统可能会在 BIOS（或 CSM）模式下启动。如果系统未以所需的模式（UEFI 与 BIOS）启动，请参阅主板的手册。 
### 4. 连接到互联网
- 若要在实时环境中设置网络连接，请执行以下步骤：
1. 确保您的网络接口已列出并启用，例如使用 ip-link ：
```
# ip link
```
2. 对于无线和 WWAN，请确保卡未被 rfkill 阻止。
3. 连接到网络：
   - 以太网 — 插入电缆。
   - Wi-Fi - 使用 iwctl 向无线网络进行身份验证。
4. 配置网络连接：
   - DHCP：动态 IP 地址和 DNS 服务器分配（由 systemd-networkd 和 systemd-resolve 提供）应该适用于以太网、WLAN 和 WWAN 网络接口。
5. 可以使用 ping 验证连接：
```
# ping archlinux.org
```
*注意：在安装映像中，默认情况下，**systemd-networkd**、**systemd-resolved**、**iwd** 和 **ModemManager** 处于**预配置**和**启用状态**。对于已安装的系统，情况并非如此。*
- **网络连接补充**
1. 确保您的网络接口已列出并启用，例如使用 ip-link ：
```
# ip link
```
2. 为了使用 systemd-networkd 连接到无线网络，需要配置了其他应用程序（如 wpa_supplicant 或 iwd）的无线适配器。
```
/etc/systemd/network/25-wireless.network
----------------------------------------
[Match]
Name=wlp2s0

[Network]
DHCP=yes
IgnoreCarrierLoss=3s
```
3. wpa_supplicant
   1. 安装 wpa_supplicant 包，其中包括主程序wpa_supplicant、密码工具wpa_passphrase和文本前端wpa_cli。
   2. 连接到加密无线网络的第一步是wpa_supplicant从 WPA 身份验证器获取身份验证。为此，必须配置wpa_supplicant，以便能够将正确的凭据提交到身份验证器。
通过身份验证后，您需要分配一个 IP 地址，请参阅网络配置#IP 地址。
   3. 与wpa_cli联系<br>
   这种连接方法允许使用wpa_cli扫描可用网络，这是一种可用于配置wpa_supplicant的命令行工具。详见wpa_cli（8）。
为了使用 wpa_cli，必须为 wpa_supplicant 指定一个控制接口，并且必须授予它更新配置的权限。为此，请创建一个最小的配置文件：
```
/etc/wpa_supplicant/wpa_supplicant.conf
----------------------------------------
ctrl_interface=/run/wpa_supplicant
update_config=1
```
   4. 列出网络接口
有线和无线接口名称都可以通过 `ls /sys/class/net` 或 `ip link`找到。

