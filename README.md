# 无线充电热控数据库（K80 Pro / miro）

Redmi K80 Pro（miro）无线充电热控完整数据库，全部数据来自设备本身（设备树 + 解密后的热控配置）。

## 内容

- `无线充电热控数据库.md`：温度 → 等级 → 电流/功率表、26 个充电场景对比、虚拟温度公式、117 个场景清单
- `无线充电热控数据库.xlsx`：同数据的 Excel 版（7 个工作表，公式联动）

## 数据链路

```
物理传感器（电池/PA/充电IC/CPU/静音/WiFi）→ 虚拟皮肤温度（5 方向加权平均）
  → thermal-engine 按场景查阈值 → wireless_ctrl_limit（等级）
    → 驱动查 wireless_thermal 表 → 各档位 voter 投电流 → MCA 取最低票生效
```

## 数据来源

- 等级→电流：设备树 `mca_charger_thermal/wireless_thermal`
- 温度→等级：`/vendor/etc/thermal-map.conf` + `/odm/etc/thermal-*.conf`
- 配置文件为 AES-128-CBC 加密，key/IV = `thermalopenssl.h`（工具：helloklf/vtools mi-thermal-config / hdzungx/ThermalMunch）
