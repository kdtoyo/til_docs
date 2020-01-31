
# Ubuntu18.04でマウスやキーボード(入力装置)が反応しない場合の復旧方法

ubuntu18.04でマウスやキーボードが反応しなくなることがありました。
現象が同じかどうかわかりませんが、復旧の一役となれば。

## 現象を確認する

xrdpを入れた辺りかも知れませんが、いつの間にやら立ち上げると、
接続しているキーボード・マウスがまったく無反応。

まずはsshで入るなどして、ログを確認してみるとよいです。
- /var/log/
→syslogとか
~~~
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) XINPUT: Adding extended input device "Logitech MX Master 2S" (type: MOUS
E, id 12)
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (**) Option "AccelerationScheme" "none"
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (**) Logitech MX Master 2S: (accel) selected scheme none/0
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (**) Logitech MX Master 2S: (accel) acceleration factor: 2.000
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (**) Logitech MX Master 2S: (accel) acceleration threshold: 4
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) event5  - Logitech MX Master 2S: is tagged by udev as: Keyboard Mouse
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) event5  - Logitech MX Master 2S: device is a pointer
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) event5  - Logitech MX Master 2S: device is a keyboard
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) config/udev: Adding input device Logitech MX Master 2S (/dev/input/mouse
0)
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) No input driver specified, ignoring this device.
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) This device may have been added with another device file.
Jan 31 12:15:53 mypc /usr/lib/gdm3/gdm-x-session[2776]: (II) config/udev: Adding input device HDA Intel PCH Front Mic (/dev/input/eve
nt6)
~~~
こういうログがでてないでしょうか。
No input driver とかでてます。

## HWEをインストールしましょう

HWE(Hardware Enablement)をインストールします。xserverでハンドリングする為の関連ライブラリも入るようです。
~~~
 $ sudo apt install xserver-xorg-hwe-18.04
 $ reboot
~~~
これで反応するようになりました。

