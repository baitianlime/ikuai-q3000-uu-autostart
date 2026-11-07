# 爱快 Q3000 · 官方底包 + 网易 UU 开机自启

基于爱快官方 **IK-Q3000 / IK-MT7981V1-Q3000 3.7.26**（Build202609111742）rootfs，注入网易 UU 插件，并挂上官方 `oemrc` 钩子实现开机自启。

## 适合谁

- 想继续用爱快原厂系统，又想用网易 UU 加速路由器插件
- 希望刷机后 UU 自动起来，少手动折腾
- **不需要** Clash / mihomo / Docker / 透明代理等额外改机能力

## 下载

请到本仓库 [**Releases**](../../releases) 下载最新包（约 28.3 MB），不要只 clone 仓库指望里面有 `.bin`（大固件以 Release 资产发布）。

| 文件 | 说明 |
|------|------|
| `IK-Q3000-3.7.26-official-with-uu-autostart-uboot.bin` | U-Boot 刷机用固件 |
| `*.sha256` | SHA-256 校验 |

当前校验（v1.0.0）：

```
560703c4aff263087d291e3eabc8621ccd2d88b8fd4f12a732b127515ba96e01
```

## 本包内容

| 项目 | 说明 |
|------|------|
| 底包 | 爱快官方 3.7.26（Build202609111742） |
| UU | `uuplugin` **v12.1.18** + `/etc/uu.conf` |
| 自启 | `/etc/oemrc` 的 `boot_end`：开机约 **20 秒**后拉起 UU |
| 不含 | Clash / mihomo / Docker / 代理管理页 / 透明代理 |
| 体积 | 单文件约 29.6 MB，低于常见 64MB firmware 分区上限 |

## 刷机方式（U-Boot）

**请只用本仓库的 `*-uboot.bin` 走 U-Boot。不要用网页升级硬塞未重算头的包。**

1. 电脑网线接 Q3000 的 **LAN**，电脑 IP 设为与 U-Boot 同网段（常见 `192.168.1.x`，以你机器 U-Boot 页为准）。
2. **断电**，按住 **Reset** 再上电，进入 U-Boot 刷机页（常见地址 `http://192.168.1.1`；部分机型恢复页需密码，以你设备为准）。
3. 上传：
   `IK-Q3000-3.7.26-official-with-uu-autostart-uboot.bin`
4. 等待重启约 1–2 分钟。爱快后台常见为 `http://192.168.9.1`（出厂常见 `admin` / `admin`，以你设备为准）。
5. 开机约 20 秒后 UU 进程会自启。手机安装 **网易 UU 加速器** App → 安装 / 绑定路由器插件。

### 校验

```bash
sha256sum -c IK-Q3000-3.7.26-official-with-uu-autostart-uboot.bin.sha256
```

### 手动启停（可选，SSH / 控制台）

```bash
/etc/oemrc start
/etc/oemrc stop
```

日志：`/tmp/uu/uuplugin.log`

## 风险与声明

- 改机固件，刷写有**变砖风险**；不熟请先确认能进 U-Boot，并自行备份。
- 与爱快官方、网易 UU **无隶属关系**；UU 账号、加速服务、合规与收费以官方为准。
- 仅供个人研究与学习；请遵守当地法律法规与运营商规定。

## 版本

| 版本 | 说明 |
|------|------|
| 1.0.0 | 官方 3.7.26 + uuplugin 12.1.18 + oemrc 自启 |

## License

仓库文档与打包脚本以 **MIT** 授权。爱快固件与网易 UU 插件版权归各自权利人所有；本仓库不转让其权利。
