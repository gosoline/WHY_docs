<!-- @format -->

# gdm修改登录界面分辨率

修改桌面登录界面的分辨率,GDM(GNOME Display Manager)是专门管理图形登录界面的,修改它的分辨率即可.

## 步骤

修改/var/lib/gdm/.config/monitors.xml 这个配置文件,可以改变登录界面的分辨率.

/var/lib/gdm/.config/monitors.xml 这个文件默认是不存在的,我们可以通过登录用户,通过设置用户的显示分辨率来生成这个文件.

1. 登录用户,设置用户的显示分辨率,并保存.
2. 打开终端,拷贝 monitors.xml 文件到/var/lib/gdm/.config：

```shell
cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml
```

3. 修改文件权限及配置

```shell
chown gdm.gdm /var/lib/gdm/.config/monitors.xml
```

生成的 monitors.xml 文件内容如下,如果需要修改分辨率,只需要修改 width 和 height 即可:

```xml
<monitors version="2">
  <configuration>
    <logicalmonitor>
      <x>0</x>
      <y>0</y>
      <scale>1</scale>
      <primary>yes</primary>
      <monitor>
        <monitorspec>
          <connector>Virtual1</connector>
          <vendor>unknown</vendor>
          <product>unknown</product>
          <serial>unknown</serial>
        </monitorspec>
        <mode>
        <!-- 修改分辨率 -->
          <width>1920</width>
          <height>1200</height>
          <rate>59.884601593017578</rate>
        </mode>
      </monitor>
    </logicalmonitor>
  </configuration>
</monitors>

```

4. 注销用户,回到登录界面,即可看到修改后的登录界面分辨率.
