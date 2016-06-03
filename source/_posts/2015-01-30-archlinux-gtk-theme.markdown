---
layout: post
title: "ArchLinuxのデスクトップをカスタマイズしてみた"
date: 2015-01-30
comments: true
categories: os
tags: arch
---
<img src="{{ root_url }}/images/more.png" alt="phoenix-power" align="left" width="100" height="100">`gtk`, `awesome`, `spacefm`あたりの設定です。<!--more--><br clear="all">


こんな感じです。ブラウザとかの表示も`gtk`の`themes`や`icons`を適用してるので、ちょっとだけOSっぽくなっています。やはり、メインマシンに直接インストールするとなると、ここらへんは気になるところです。`arch`だと少しだけやる気が出ますね。最初から`x`がカスタマイズされてるOSよりは、`x`すら入ってないOSのほうが、必要に迫られて中身を見るようになるので。

![](http://lh3.ggpht.com/-o3-sey5BB_w/VMpTHZZnnII/AAAAAAAAAU0/2TtaO0n3E14/s0/2015-01-29-052142615.png)

##awesome

ウィンドウマネージャーです。愛用しています。

![](http://lh4.ggpht.com/-z2BihCab60g/VMpTF4s-bYI/AAAAAAAAAUo/SI2LgJahx_s/s0/2015-01-29-052142615.png)


[powerarrow](https://github.com/romockee/powerarrow)を使います。

![](http://lh3.ggpht.com/-LBL29Ersp8c/VMpTC-hJvdI/AAAAAAAAAT8/MZxFjp8hpiE/s0/2015-01-29-052142615.png)

{% codeblock lang:bash %}
$ yaourt -S luacairo
$ sudo pacman -S vicious
$ git clone https://github.com/bioe007/awesome-revelation ~/.config/awesome/revelation 
$ git clone https://github.com/copycat-killer/lain ~/.config/awesome/lain

$ git clone https://github.com/syui/powerarrow-dark

$ cd powerarrow-dark

$ cp -R awesome/ ~/.config
{% endcodeblock %}

https://github.com/syui/powerarrow-dark

https://github.com/esn89/powerarrow-dark

https://raw.githubusercontent.com/mikar/awesome34-themes/master/arch/wallpaper_kiss_montecarlo_1600x900.png

###rc.lua

スクリーンショットを撮影するための設定とかです。

{% codeblock lang:lua ~/.config/awesome/rc.lua %}
-- library
-- 使わないならコメントアウトします
-- local reverse = require("revelation")
-- local lain = require("lain")

-- screenshot
-- maim, slop, mcomixを使います
util.spawn_with_shell("maim ~/Pictures/screenshot/`date +%F-%N`.png") end),
    awful.key({ modkey ,"Shift"}, "5", function () awful.util.spawn_with_shell("maim -s ~/Pictures/screenshot/`date +%F-%N`.png") end),
    awful.key({ modkey ,"Shift"}, "6", function () awful.util.spawn_with_shell("maim -i `xdotool getactivewindow` ~/Pictures/screenshot/`date +%F-%N`.png") end),
    awful.key({ modkey ,"Shift"}, "7", function () awful.util.spawn_with_shell("mcomix ~/Pictures/screenshot/") end),
{% endcodeblock %}

###theme.lua

{% codeblock lang:lua %}
-- fullscreenにした時にtaglistを非表示にするには、コメントアウトします
-- Display the taglist squares
--theme.taglist_squares_sel   = pathToConfig .. "powerarrowf/icons/square_sel.png"
--theme.taglist_squares_unsel = pathToConfig .. "powerarrowf/icons/square_unsel.png"
{% endcodeblock %}

##spacefm

[spacefm](https://github.com/IgnorantGuru/spacefm)もデフォルトテーマがあれなので、テーマを当ててみます。テーマは、[numix](https://github.com/shimmerproject/Numix)辺りが良さげ。[gtk](https://wiki.archlinux.org/index.php/GTK%2B)。ファイルマネージャーです。愛用しています。

![](http://lh4.ggpht.com/-mmtLMlic0jw/VMpTDF41m4I/AAAAAAAAAUI/e27egEH_Kqc/s0/2015-01-29-052142615.png)

{% codeblock lang:bash %}
$ yaourt -S numix-icon-theme-git
$ sudo pacman -S numix-themes

$ vim ~/.gtkrc-2.0
{% endcodeblock %}

{% codeblock lang:bash ~/.gtkrc-2.0 %}
gtk-icon-theme-name = "Numix"
gtk-theme-name = "Numix"
gtk-font-name = "DejaVu Sans 13"
{% endcodeblock %}

`/usr/share/icons/Numix`と`/usr/share/themes/Numix`にあるファイルを使います。

##nautilus

ここで、有名な`gnome-nautilus`と比べてみましょう。こちらもファイルマネージャーですが、個人的には使っていません。これは、`gtk-3`を使ってますので、`~/.config/gtk-3.0/settings.ini`を用意します。

![](http://lh3.ggpht.com/-1qpWdaRtEFE/VMpTIG9Q64I/AAAAAAAAAVA/lcKnDPzTnEI/s0/2015-01-29-052142615.png)

カスタマイズしたい人は、上記と同じように、適当にテーマ、アイコンをダウンロードしてきて設定しましょう。

![](http://lh4.ggpht.com/-qJzS0rcGByY/VMpTG032Y4I/AAAAAAAAAU8/cTF3_ypuQqE/s0/2015-01-29-052142615.png)

{% codeblock lang:bash %}
{% raw %}
$ mkdir -p ~/.config/gtk-3.0

$ cat << EOF > $!/settings.ini
gtk-icon-theme-name = "Default"
#gtk-icon-theme-name = "Numix-Light"
gtk-theme-name = "Numix"
gtk-font-name = "DejaVu Sans 13"
EOF

$ gtk-update-icon-cache -f /usr/share/icons/Default
{% endraw %}
{% endcodeblock %}

##conky

[https://wiki.archlinux.org/index.php/Conky](https://wiki.archlinux.org/index.php/Conky)

`conky`もカスタマイズしていこうかな。

[https://github.com/51114u9/conky-themes](https://github.com/51114u9/conky-themes)

[https://github.com/51114u9/conky-themes/blob/master/slackware-conky-google-now-dark/INSTALL.md](https://github.com/51114u9/conky-themes/blob/master/slackware-conky-google-now-dark/INSTALL.md)

しかし、`conky`辺りは、上手く言えないけど、あまり色々入れるのはよくなさそうに思います。`.zip`で配布されているもの多いですし。`.conkyrc`で公開してくれればありがたいのですが。

[http://icanbeacoder.com/blog/infinity-conky-version-2/](http://icanbeacoder.com/blog/infinity-conky-version-2/)

{% codeblock lang:bash ~/.conkyrc %}
{% raw %}
# Conky theme put together by Culinax
# Part of the Manjaro Awesome WM Respin

background no
own_window yes
own_window_type override
own_window_hints undecorated,below,skip_taskbar,skip_pager,sticky
own_window_argb_visual yes
own_window_argb_value 200
default_color 000000
alignment top_right
gap_x 18
gap_y 36
use_xft yes
xftfont Terminus:size=9
uppercase no
update_interval 2
total_run_times 0
double_buffer yes
no_buffers yes
cpu_avg_samples 2
draw_shades no
draw_outline no
draw_borders no
minimum_size 215 525
maximum_width 250

color1 447799
color2 9eb1ba
color3 ffffff

TEXT
# system date
# gnu/linux distro
${color1}${font Open Sans Light:size=15}${exec grep "^ID=" /etc/os-release | sed -e "s/^ID=\(.*\)$/\1/g" | sed -r "s/\b(.)/\U\1/g"} ${sysname} ${exec grep "^VERSION_ID=" /etc/os-release | sed -e "s/^VERSION_ID=\(.*\)$/\1/g"}${hr}${color}${font}

# kernel version & arch
${goto 65}${color4}v. ${kernel}${color}  on  ${color4}${machine} bits${color}

${color1}CLOCK${hr}
${color2}${time %d %B %Y}${alignr}${color3}${font Terminus:size=12}${time %H:%M}${font}  

${color1}MANJAROLINUX${hr}
${color2}Host:${alignr}${color3}${nodename}
${color2}Kernel:${alignr}${color3}${kernel}
${color2}Uptime:${alignr}${color3}${uptime}
${color2}CPU:${alignr}${color3}${cpu cpu0}%
${color2}RAM:${alignr}${color3}${mem} / ${memmax}

${color1}PROCESSES${hr}
${color2}${top_mem name 1}${alignr}${color3}${top_mem mem 1}
${color2}${top_mem name 2}${alignr}${color3}${top_mem mem 2}
${color2}${top_mem name 3}${alignr}${color3}${top_mem mem 3}
${color2}${top_mem name 4}${alignr}${color3}${top_mem mem 4}

# system info
${color1}User: ${uid_name 1000}${hr}
${alignr}Machine: ${color4}${nodename}
Uptime: ${color4}${uptime_short} ${alignr}${loadavg}${color}
RAM: ${color4}${mem}${color} / ${color4}${memmax}${color} - ${color4}${memperc}% ${voffset 2}${membar 6}${color}
Swap: ${color4}${swap}${color} / ${color4}${swapmax}${color} - ${color4}${swapperc}% ${voffset 2}${swapbar 6}${color}
Root: ${color4}${fs_used /}${color} / ${color4}${fs_size /}${color} - ${color4}${voffset 2}${fs_bar 6 /}${color}
Data: ${color4}${fs_used /mnt/datos}${color} / ${color4}${fs_size /mnt/datos}${color} - ${color4}${voffset 2}${fs_bar 6 /mnt/datos}${color}
Battery: ${color4}${battery_percent BAT1}%${color}${alignr}AC Adapter: ${color4}${acpiacadapter}${color}

CPU: ${color4}${cpu}%${color}${alignr}Temp: ${color4}${acpitemp}° C${color}
${tab}${tab}CPU 1:${tab}${tab}${color4}${freq_g 0}${color} Ghz${alignr}${color4}${cpu cpu0}${color} %
${tab}${tab}CPU 2:${tab}${tab}${color4}${freq_g 1}${color} Ghz${alignr}${color4}${cpu cpu1}${color} %
${tab}${tab}CPU 3:${tab}${tab}${color4}${freq_g 2}${color} Ghz${alignr}${color4}${cpu cpu2}${color} %
${tab}${tab}CPU 4:${tab}${tab}${color4}${freq_g 3}${color} Ghz${alignr}${color4}${cpu cpu3}${color} %
${alignr}${cpugraph 20,230 CE5C00 A40000 -t}${color}${voffset -10}
# network
${if_up wlan0}WiFi:
${tab}${tab}Strength: ${color4}${wireless_link_qual_perc wlan0} %${color}${alignr}Essid: ${color4}${wireless_essid wlan0}${color}
${tab}${tab}Download: ${color4}${downspeed wlan0}${color}${alignr}Upload: ${color4}${upspeed wlan0}${color}
${tab}${tab}Public IP:${alignr}${color4}${execi 3600 wget -q -O /dev/stdout http://checkip.dyndns.org/ | cut -d : -f 2- | cut -d \< -f -1 | sed 's/^ *//g'}${color}
${tab}${tab}Local  IP:${alignr}${color4}${addr wlan0}${color}${endif}
${if_up eth0}Wired:
${tab}${tab}Download: ${color4}${downspeed eth0}${color}${alignr}Upload: ${color4}${upspeed eth0}${color}
${tab}${tab}Public IP:${alignr}${color4}${execi 3600 wget -q -O /dev/stdout http://checkip.dyndns.org/ | cut -d : -f 2- | cut -d \< -f -1 | sed 's/^ *//g'}${color}
${tab}${tab}Local  IP:${alignr}${color4}${addr eth0}${color}${endif}
${if_up wlan0}${else}${if_up eth0}${else}${voffset -20}${color7}Network Unavailable!${tab}${tab}:(${color}${voffset 20}${endif}${endif}
${voffset -92}
{% endraw %}
{% endcodeblock %}


