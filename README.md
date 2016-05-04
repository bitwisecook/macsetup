# Setting up a new Mac

## Installing software

 * Karabiner
   * fix annoyances with UK keyboard layout
 * Dropbox
 * 1Password
 * XCode
 * iStatMenus
 * Homebrew
   * pngcrush
   * ssh-copy-id
   * sqlite3
   * python 3.x
   * python 2.x
 * Python
   * virtualenvwrapper  
 * Omnigraffle Pro
 * Sublime text 3
 * Wireshark
 * iTerm2
 * IDEA based IDEs
   * IDEs
     * Pycharm
     * IDEA
     * cLion
     * Rubymine
     * Webstorm
     * Datagrip
   * Plugins
     * Settings Repository
     * https://github.com/bitwisecook/ideasettings.git
 * SourceTree
 * Office
 * Whitebox Packages
 
## Shell

### Hostname
`read -p "hostname: " n ; sudo scutil --set ComputerName "$n" ; sudo scutil --set LocalHostName "$n" ; sudo scutil --set HostName "$n"`  

### Permit VMs to get NTP
`sudo launchctl unload /System/Library/LaunchDaemons/org.ntp.ntpd.plist`  
`sudo bash -c "echo restrict 172.18.40.0/24>>/etc/ntpd-restrict.conf"`  
`sudo launchctl load /System/Library/LaunchDaemons/org.ntp.ntpd.plist`  

### Setup Sublime Text
`ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" ~/bin/subl`  
`defaults write com.apple.LaunchServices/com.apple.launchservices.secure LSHandlers -array-add '{LSHandlerContentType=public.plain-text;LSHandlerRoleAll=com.sublimetext.3;}'`

### Setup Homebrew
```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install advancecomp augeas autoconf automake bash bash-completion binwalk boot2docker colordiff colormake dialog docker dos2unix fswatch gnu-tar go isl jq libxml2 libyaml mpfr node oniguruma openssl optipng p7zip pngcrush psutils pv python python3 readline redis rgxg rlwrap shiboken sqlite ssdeep ssh-copy-id sudolikeaboss the_silver_searcher ucl unar upx watch xz zopfli
```

### Setup VMware Fusion Networking
`sudo vim /Library/Preferences/VMware\ Fusion/networking`  
```
VERSION=1,0
answer VNET_1_DHCP yes
answer VNET_1_DHCP_CFG_HASH E297974CBBDEEE9E9A9413E55B73A4B3E7350A11
answer VNET_1_HOSTONLY_NETMASK 255.255.255.0
answer VNET_1_HOSTONLY_SUBNET 192.168.40.0
answer VNET_1_VIRTUAL_ADAPTER yes
answer VNET_2_DHCP yes
answer VNET_2_DHCP_CFG_HASH 618A207B31DFA1520E7A400494C6FF2EFF023C4B
answer VNET_2_HOSTONLY_NETMASK 255.255.255.0
answer VNET_2_HOSTONLY_SUBNET 10.10.5.0
answer VNET_2_VIRTUAL_ADAPTER yes
answer VNET_3_DHCP yes
answer VNET_3_DHCP_CFG_HASH 4602001036590A869AAB7CBC860272FD6BBC4403
answer VNET_3_HOSTONLY_NETMASK 255.255.255.0
answer VNET_3_HOSTONLY_SUBNET 172.16.5.0
answer VNET_3_VIRTUAL_ADAPTER yes
answer VNET_4_DHCP yes
answer VNET_4_DHCP_CFG_HASH D7B48893D70B33CD6A5A94D3BAF6C60DC816B789
answer VNET_4_HOSTONLY_NETMASK 255.255.255.0
answer VNET_4_HOSTONLY_SUBNET 172.17.5.0
answer VNET_4_VIRTUAL_ADAPTER yes
answer VNET_5_DHCP yes
answer VNET_5_DHCP_CFG_HASH 342ABD172E1237CBA668246D6D90E4C49FB41F96
answer VNET_5_HOSTONLY_NETMASK 255.255.255.0
answer VNET_5_HOSTONLY_SUBNET 172.18.5.0
answer VNET_5_VIRTUAL_ADAPTER yes
answer VNET_8_DHCP yes
answer VNET_8_DHCP_CFG_HASH D0913C716798B5BA9210F47A4B8F45ADDBFA90CD
answer VNET_8_HOSTONLY_NETMASK 255.255.255.0
answer VNET_8_HOSTONLY_SUBNET 172.18.40.0
answer VNET_8_NAT yes
answer VNET_8_VIRTUAL_ADAPTER yes
```

### Setup Karabiner

#### Screensaver on Cmd-L
```xml
<?xml version="1.0"?>
<root>
  <!-- Place this file to ~/Library/Application Support/Karabiner/private.xml -->
  <item>
    <item>
      <name>Screensaver Lock screen (Cmd-L)</name>
      <identifier>myconfig.lock</identifier>
      <autogen>__KeyToKey__ KeyCode::L, ModifierFlag::COMMAND_L | ModifierFlag::NONE, KeyCode::VK_OPEN_URL_APP_ScreenSaverEngine</autogen>
      <autogen>__KeyToKey__ KeyCode::L, ModifierFlag::COMMAND_R | ModifierFlag::NONE, KeyCode::VK_OPEN_URL_APP_ScreenSaverEngine</autogen>
    </item>
  </item>
</root>
```

```sh
#!/bin/sh

cli=/Applications/Karabiner.app/Contents/Library/bin/karabiner

$cli set myconfig.lock 1
/bin/echo -n .
$cli set repeat.initial_wait 200
/bin/echo -n .
$cli set repeat.wait 22
/bin/echo -n .
$cli set remap.iso_swap_tilda_section 1
/bin/echo -n .
/bin/echo
```
