# 公众号排版组件库 —— 文献共读

> **使用说明**：本组件库为「文献共读（Literature Co-read）」主题，所有组件使用**内联样式**，可直接复制粘贴到微信公众号编辑器。
>
> **设计风格**：参考医疗/学术「文献共读」栏目——**深蓝系列封面** + **紫色题框** + **海军蓝分节竖条**，正文灰阶、轻阴影、中小圆角。专为 **IMRaD**（研究目的 / 方法 / 结果 / 结论）骨架、解剖图 A/B/C 图注、文献摘要与【文献来源】脚注设计。气质克制专业、信息密度中高。
>
> **公众号平台限制须知**：
> - ❌ 不支持 `<style>`/`<script>`、CSS class/id/`<div>`、`position:fixed/absolute/sticky`、`float`、`@media`/`@keyframes`、`display:grid`、CSS 变量
> - ✅ 支持内联 `style`、`display:flex`（有限）、`linear-gradient`、`border-radius`、`box-shadow`、`<section>/<p>/<span>/<strong>/<img>` 等基础标签
>
> **WeChat 兼容铁律**（本主题组件全部已按此写好，改动时必须遵守）：
> - 所有"装饰性空元素"（分割线、竖条、进度条填充）**必须在内部放 `<span leaf=""><br></span>` 占位**
> - **不要把 `font-size`/`border-bottom` 打在 `<strong>` 上**，也不要在同一个 `<p>` 里混多个不同 `font-size`
> - 不用 `position:absolute`；结构化区域无内容时**整块删掉**

---

## 设计变量速查表

```
主色（海军蓝）：     #001E5B（分节/编号/锚点）
系列封面深蓝：       #0A1654
强调色（紫）：       #69318E（题框描边/摘要左条/次强调）
装饰淡紫：           #C4B5FD（关键词下划线 / 浅强调）
浅紫底：             #F3E8FF / #F5F4F8 / #F8F7FC
海军浅底：           #EEF1F8
边框线：             #D6DCEB / #E5E5E5 / #DBDBDB
标题色：             #001E5B
正文色：             #3E3E3E
次要文字：           #5E5E5E
弱化文字：           #A0A0A0
纯白底：             #FFFFFF
正文字号：           15px
行高：               1.85
字间距：             1px（正文）
最大宽度：           677px
圆角：               6~10px
阴影：               轻（题框 0 0 10px #DBDBDB；图卡可极轻）
```

字体栈：`-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif`

**正文关键词下划线**（theme-index 权威值）：`border-bottom:2px solid #C4B5FD;font-weight:600;`

---

## 组件 1 全局容器

```html
<section style="max-width:677px;margin:0 auto;background:#FFFFFF;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#3E3E3E;line-height:1.8;letter-spacing:0.5px;overflow-x:hidden;">

  <!-- 所有组件放在这里 -->

</section>
```

---

## 组件 2 系列封面刊头 series-cover

**用途**：栏目系列开篇（对应参考文「文献共读」深蓝封面）。全文最多 1 处，放最前；若平台已设封面图且用户不要正文内刊头，可整块删除。

**可替换**：`{{系列名}}`（默认「文献共读」）`{{副说明}}`

```html
<section style="background:#0A1654;padding:40px 24px 36px;text-align:center;overflow:hidden;margin:0 0 24px;">
  <p style="margin:0 0 18px;font-size:11px;letter-spacing:3px;color:rgba(255,255,255,0.55);">
    <span leaf="">SERIES · LITERATURE</span>
  </p>
  <p style="margin:0 0 10px;font-size:22px;font-weight:700;color:#FFFFFF;letter-spacing:4px;">
    <span leaf="">📚  {{系列名}}</span>
  </p>
  <p style="margin:0;font-size:12px;color:rgba(255,255,255,0.65);letter-spacing:1px;">
    <span leaf="">{{副说明}}</span>
  </p>
</section>
```

---

## 组件 3 文献题框卡 title-frame

**用途**：文章主标题（紫框圆角卡，参考文标题容器）。可含系列前缀「文献共读 | …」。

**可替换**：`{{栏目小标}}` `{{主标题}}`

```html
<section style="margin:0 10px 24px;border:2px solid #69318E;border-radius:10px;overflow:hidden;background:#FFFFFF;box-shadow:0 0 10px 0 #DBDBDB;">
  <section style="padding:16px 18px;">
    <p style="margin:0 0 8px;font-size:11px;color:#69318E;font-weight:700;letter-spacing:2px;">
      <span leaf="">{{栏目小标}}</span>
    </p>
    <p style="margin:0;font-size:16px;font-weight:700;color:#001E5B;line-height:1.65;letter-spacing:1px;">
      <span leaf="">{{主标题}}</span>
    </p>
  </section>
</section>
```

---

## 组件 4 背景导读 background-lead

**用途**：病种/术式背景科普段（参考文开篇 FAI 说明）。

```html
<section style="padding:0 20px 24px;">
  <p style="margin:0 0 8px;font-size:13px;font-weight:700;color:#001E5B;letter-spacing:1px;">
    <span leaf="">{{导读小标，可删整行}}</span>
  </p>
  <p style="margin:0;font-size:15px;line-height:1.85;color:#3E3E3E;text-align:justify;letter-spacing:1px;">
    <span leaf="">{{背景导读正文}}</span>
  </p>
</section>
```

---

## 组件 5 图注三列 A/B/C figure-abc

**用途**：解剖/术式示意图 + A/B/C 图注（参考文标准件）。无图注说明时只保留图片区。

```html
<section style="padding:0 10px 24px;">
  <section style="border:1px solid #DBDBDB;border-radius:8px;overflow:hidden;background:#FAFAFA;padding:12px;">
    <span leaf=""><img src="{{图片URL}}" alt="示意图" style="max-width:100%;height:auto;display:block;margin:0 auto;border-radius:4px;"></span>
  </section>
  <section style="display:flex;margin-top:12px;">
    <section style="flex:1;text-align:center;padding:8px 4px;">
      <p style="margin:0 0 4px;font-size:12px;font-weight:800;color:#001E5B;"><span leaf="">A</span></p>
      <p style="margin:0;font-size:11px;color:#5E5E5E;line-height:1.5;"><span leaf="">{{图注A}}</span></p>
    </section>
    <section style="flex:1;text-align:center;padding:8px 4px;border-left:1px solid #E5E5E5;border-right:1px solid #E5E5E5;">
      <p style="margin:0 0 4px;font-size:12px;font-weight:800;color:#001E5B;"><span leaf="">B</span></p>
      <p style="margin:0;font-size:11px;color:#5E5E5E;line-height:1.5;"><span leaf="">{{图注B}}</span></p>
    </section>
    <section style="flex:1;text-align:center;padding:8px 4px;">
      <p style="margin:0 0 4px;font-size:12px;font-weight:800;color:#001E5B;"><span leaf="">C</span></p>
      <p style="margin:0;font-size:11px;color:#5E5E5E;line-height:1.5;"><span leaf="">{{图注C}}</span></p>
    </section>
  </section>
</section>
```

仅两项时改为两列，删掉 C 列及中间多余边框。

---

## 组件 6 重申标题 restated-title

**用途**：示意图后再次加粗点题（参考文结构）。

```html
<section style="padding:0 20px 24px;">
  <p style="margin:0;font-size:15px;font-weight:800;color:#001E5B;line-height:1.7;text-align:center;letter-spacing:0.5px;">
    <span leaf="">{{重申标题}}</span>
  </p>
</section>
```

---

## 组件 7 IMRaD 分节标题 imrad-heading

**用途**：研究目的 / 研究方法 / 研究结果 / 研究结论。本主题默认主力分节样式。

**可替换**：`{{EN标签}}`（OBJECTIVE / METHODS / RESULTS / CONCLUSION）`{{中文标题}}`

```html
<section style="margin-top:28px;margin-bottom:16px;padding:0 10px;">
  <section style="display:flex;align-items:center;">
    <section style="width:8px;height:28px;background:#001E5B;border-radius:2px;margin-right:12px;flex-shrink:0;">
      <span leaf=""><br></span>
    </section>
    <section>
      <p style="margin:0 0 2px;font-size:10px;font-weight:700;color:#69318E;letter-spacing:2px;">
        <span leaf="">{{EN标签}}</span>
      </p>
      <p style="margin:0;font-size:17px;font-weight:800;color:#001E5B;letter-spacing:1px;">
        <span leaf="">{{中文标题}}</span>
      </p>
    </section>
  </section>
</section>
```

**常用映射**：
| 中文 | EN |
|------|-----|
| 研究目的 | OBJECTIVE |
| 研究方法 | METHODS |
| 研究结果 | RESULTS |
| 研究结论 | CONCLUSION |
| 文献摘要 | ABSTRACT |

---

## 组件 8 章节编号标题 section-title

**用途**：非 IMRaD 的通用大章节（背景、讨论、临床启示等）。

```html
<section style="margin-top:32px;margin-bottom:20px;padding:0 10px;">
  <section style="border-bottom:2px solid #001E5B;padding-bottom:12px;">
    <section style="display:flex;align-items:center;">
      <span style="display:inline-block;background:#001E5B;color:#FFFFFF;font-size:14px;font-weight:800;padding:4px 12px;border-radius:4px;margin-right:12px;line-height:1.3;"><span leaf="">{{编号}}</span></span>
      <section>
        <p style="margin:0 0 2px;font-size:10px;color:#69318E;font-weight:700;letter-spacing:2px;"><span leaf="">{{ENGLISH TAG}}</span></p>
        <p style="margin:0;font-size:17px;font-weight:800;color:#001E5B;"><span leaf="">{{中文章节标题}}</span></p>
      </section>
    </section>
  </section>
</section>
```

结语编号可用 `∞` 或 `///`。

---

## 组件 9 子节左竖条 subhead

```html
<p style="font-size:15px;font-weight:800;color:#001E5B;margin:24px 20px 12px;padding-left:10px;border-left:3px solid #69318E;line-height:1.4;">
  <span leaf="">{{子标题}}</span>
</p>
```

---

## 组件 10 正文段落 paragraph

> 每段主动标 1~3 处淡紫下划线关键词。

**基础**：

```html
<p style="margin:0 20px 18px;font-size:15px;line-height:1.85;color:#3E3E3E;text-align:justify;letter-spacing:1px;">
  <span leaf="">{{正文}}</span>
</p>
```

**带关键词下划线（推荐默认）**：

```html
<p style="margin:0 20px 18px;font-size:15px;line-height:1.85;color:#3E3E3E;text-align:justify;letter-spacing:1px;">
  <span leaf="">{{前半}}</span>
  <span style="border-bottom:2px solid #C4B5FD;font-weight:600;"><span leaf="">{{关键短语}}</span></span>
  <span leaf="">{{后半}}</span>
</p>
```

---

## 组件 11 行内强调 styles

### 11a 深蓝加粗（锚点 ≤5）

```html
<strong style="color:#001E5B;"><span leaf="">{{锚点词}}</span></strong>
```

### 11b 普通加粗

```html
<strong><span leaf="">{{文字}}</span></strong>
```

### 11c 浅紫概念标签

```html
<span style="background:#F3E8FF;color:#5B21B6;padding:1px 6px;border-radius:3px;font-weight:600;"><span leaf="">{{概念}}</span></span>
```

### 11d 淡紫下划线（默认关键词标记）

```html
<span style="border-bottom:2px solid #C4B5FD;font-weight:600;"><span leaf="">{{短语}}</span></span>
```

### 11e 缩写/术语胶囊

```html
<span style="background:#EEF1F8;color:#001E5B;padding:2px 6px;border-radius:3px;font-size:13px;font-weight:600;font-family:ui-monospace,Menlo,monospace;"><span leaf="">{{缩写}}</span></span>
```

---

## 组件 12 文献摘要条 abstract-block

```html
<section style="margin:8px 10px 24px;background:#F5F4F8;border-left:4px solid #69318E;border-radius:0 8px 8px 0;padding:16px 18px;">
  <p style="margin:0 0 8px;font-size:12px;font-weight:800;color:#69318E;letter-spacing:2px;">
    <span leaf="">文献摘要 · ABSTRACT</span>
  </p>
  <p style="margin:0;font-size:14px;line-height:1.85;color:#3E3E3E;text-align:justify;">
    <span leaf="">{{摘要正文}}</span>
  </p>
</section>
```

---

## 组件 13 结论金句卡 key-quote

```html
<section style="margin:0 10px 20px;background:#EEF1F8;border-left:4px solid #001E5B;border-radius:0 8px 8px 0;padding:16px 18px;">
  <p style="margin:0;font-size:15px;font-weight:700;color:#001E5B;line-height:1.8;">
    <span leaf="">「{{结论金句}}」</span>
  </p>
</section>
```

---

## 组件 14 提示 / 警示 / 达标

### 14a 信息提示

```html
<section style="margin:0 10px 20px;background:#F8F7FC;border:1px solid #E9D5FF;border-radius:8px;padding:14px 16px;">
  <p style="margin:0 0 6px;font-size:12px;font-weight:800;color:#69318E;letter-spacing:1px;">
    <span leaf="">ℹ {{标签}}</span>
  </p>
  <p style="margin:0;font-size:14px;color:#3E3E3E;line-height:1.75;">
    <span leaf="">{{说明}}</span>
  </p>
</section>
```

### 14b 阅读注意（限制/偏倚）

```html
<section style="margin:0 10px 20px;background:#FFF7ED;border-left:4px solid #C2410C;border-radius:0 8px 8px 0;padding:14px 16px;">
  <p style="margin:0 0 6px;font-size:12px;font-weight:800;color:#C2410C;">
    <span leaf="">⚠ 阅读注意</span>
  </p>
  <p style="margin:0;font-size:14px;color:#3E3E3E;line-height:1.75;">
    <span leaf="">{{限制说明}}</span>
  </p>
</section>
```

### 14c 达标/阳性发现

```html
<section style="margin:0 10px 20px;background:#F0FDF4;border-left:4px solid #15803D;border-radius:0 8px 8px 0;padding:14px 16px;">
  <p style="margin:0 0 6px;font-size:12px;font-weight:800;color:#15803D;">
    <span leaf="">✓ {{标签}}</span>
  </p>
  <p style="margin:0;font-size:14px;color:#3E3E3E;line-height:1.75;">
    <span leaf="">{{说明}}</span>
  </p>
</section>
```

### 14d 灰底旁注

```html
<section style="margin:0 10px 20px;border-left:4px solid #DBDBDB;background:#FAFAFA;border-radius:0 8px 8px 0;padding:14px 16px;">
  <p style="margin:0;font-size:14px;color:#5E5E5E;line-height:1.75;">
    <span leaf="">{{旁注}}</span>
  </p>
</section>
```

---

## 组件 15 双组对照卡 compare-card

```html
<section style="margin:0 10px 20px;background:#F5F4F8;border:1px solid #E5E5E5;border-radius:8px;padding:14px;">
  <section style="display:flex;align-items:stretch;">
    <section style="flex:1;text-align:center;padding:12px 8px;background:#001E5B;border-radius:6px;">
      <p style="margin:0 0 4px;font-size:13px;font-weight:800;color:#FFFFFF;"><span leaf="">{{组别A}}</span></p>
      <p style="margin:0;font-size:11px;color:rgba(255,255,255,0.75);line-height:1.5;"><span leaf="">{{说明A}}</span></p>
    </section>
    <section style="display:flex;align-items:center;padding:0 10px;">
      <span style="font-size:12px;font-weight:700;color:#A0A0A0;"><span leaf="">vs</span></span>
    </section>
    <section style="flex:1;text-align:center;padding:12px 8px;background:#FFFFFF;border:1px solid #DBDBDB;border-radius:6px;">
      <p style="margin:0 0 4px;font-size:13px;font-weight:800;color:#001E5B;"><span leaf="">{{组别B}}</span></p>
      <p style="margin:0;font-size:11px;color:#5E5E5E;line-height:1.5;"><span leaf="">{{说明B}}</span></p>
    </section>
  </section>
</section>
```

---

## 组件 16 指标卡 metrics

### 三列

```html
<section style="padding:0 10px;margin-bottom:20px;display:flex;">
  <section style="flex:1;text-align:center;background:#EEF1F8;border:1px solid #D6DCEB;border-radius:8px;padding:14px 8px;margin-right:8px;">
    <p style="margin:0 0 4px;font-size:22px;font-weight:900;color:#001E5B;line-height:1;"><span leaf="">{{数字1}}</span></p>
    <p style="margin:0;font-size:11px;color:#A0A0A0;"><span leaf="">{{说明1}}</span></p>
  </section>
  <section style="flex:1;text-align:center;background:#EEF1F8;border:1px solid #D6DCEB;border-radius:8px;padding:14px 8px;margin-right:8px;">
    <p style="margin:0 0 4px;font-size:22px;font-weight:900;color:#001E5B;line-height:1;"><span leaf="">{{数字2}}</span></p>
    <p style="margin:0;font-size:11px;color:#A0A0A0;"><span leaf="">{{说明2}}</span></p>
  </section>
  <section style="flex:1;text-align:center;background:#EEF1F8;border:1px solid #D6DCEB;border-radius:8px;padding:14px 8px;">
    <p style="margin:0 0 4px;font-size:22px;font-weight:900;color:#001E5B;line-height:1;"><span leaf="">{{数字3}}</span></p>
    <p style="margin:0;font-size:11px;color:#A0A0A0;"><span leaf="">{{说明3}}</span></p>
  </section>
</section>
```

### 两列

```html
<section style="padding:0 10px;margin-bottom:20px;display:flex;">
  <section style="flex:1;text-align:center;background:#F5F4F8;border:1px solid #E5E5E5;border-radius:8px;padding:16px 10px;margin-right:8px;">
    <p style="margin:0 0 4px;font-size:24px;font-weight:900;color:#69318E;line-height:1;"><span leaf="">{{数字A}}</span></p>
    <p style="margin:0;font-size:12px;color:#A0A0A0;"><span leaf="">{{说明A}}</span></p>
  </section>
  <section style="flex:1;text-align:center;background:#F5F4F8;border:1px solid #E5E5E5;border-radius:8px;padding:16px 10px;">
    <p style="margin:0 0 4px;font-size:24px;font-weight:900;color:#69318E;line-height:1;"><span leaf="">{{数字B}}</span></p>
    <p style="margin:0;font-size:12px;color:#A0A0A0;"><span leaf="">{{说明B}}</span></p>
  </section>
</section>
```

---

## 组件 17 对照表 compare-table

```html
<section style="margin:0 10px 20px;border:1px solid #DBDBDB;border-radius:8px;overflow:hidden;">
  <section style="display:flex;background:#001E5B;">
    <section style="width:34%;padding:10px 12px;"><p style="margin:0;font-size:12px;font-weight:700;color:#FFFFFF;"><span leaf="">{{维度列}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid rgba(255,255,255,0.15);"><p style="margin:0;font-size:12px;font-weight:700;color:#FFFFFF;"><span leaf="">{{方案A}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid rgba(255,255,255,0.15);"><p style="margin:0;font-size:12px;font-weight:700;color:#FFFFFF;"><span leaf="">{{方案B}}</span></p></section>
  </section>
  <section style="display:flex;background:#FFFFFF;border-bottom:1px solid #E5E5E5;">
    <section style="width:34%;padding:10px 12px;"><p style="margin:0;font-size:13px;color:#3E3E3E;"><span leaf="">{{行标题}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid #E5E5E5;"><p style="margin:0;font-size:13px;color:#001E5B;"><span leaf="">{{值A}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid #E5E5E5;"><p style="margin:0;font-size:13px;color:#001E5B;"><span leaf="">{{值B}}</span></p></section>
  </section>
  <section style="display:flex;background:#F8F7FC;">
    <section style="width:34%;padding:10px 12px;"><p style="margin:0;font-size:13px;color:#3E3E3E;"><span leaf="">{{行标题}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid #E5E5E5;"><p style="margin:0;font-size:13px;color:#001E5B;"><span leaf="">{{值A}}</span></p></section>
    <section style="width:33%;padding:10px 12px;border-left:1px solid #E5E5E5;"><p style="margin:0;font-size:13px;color:#001E5B;"><span leaf="">{{值B}}</span></p></section>
  </section>
</section>
```

行数按需增减；中间行带 `border-bottom`，末行可用浅底交替。

---

## 组件 18 有序列表 ordered-list

```html
<section style="padding:0 20px;margin-bottom:20px;">
  <section style="display:flex;align-items:flex-start;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#001E5B;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-right:10px;margin-top:2px;"><span leaf="">1</span></span>
    <p style="margin:0;font-size:15px;color:#3E3E3E;line-height:1.75;flex:1;"><span leaf="">{{列表项}}</span></p>
  </section>
  <section style="display:flex;align-items:flex-start;margin-bottom:12px;">
    <span style="display:inline-flex;align-items:center;justify-content:center;width:22px;height:22px;background:#001E5B;color:#fff;font-size:12px;font-weight:700;border-radius:50%;flex-shrink:0;margin-right:10px;margin-top:2px;"><span leaf="">2</span></span>
    <p style="margin:0;font-size:15px;color:#3E3E3E;line-height:1.75;flex:1;"><span leaf="">{{列表项}}</span></p>
  </section>
</section>
```

---

## 组件 19 研究步骤 step-label

```html
<section style="padding:0 20px;margin-bottom:18px;">
  <section style="display:flex;align-items:center;margin-bottom:8px;">
    <span style="display:inline-block;background:#001E5B;color:#fff;font-size:11px;font-weight:700;padding:2px 8px;border-radius:4px;margin-right:8px;"><span leaf="">STEP {{序号}}</span></span>
    <span style="font-size:15px;font-weight:800;color:#001E5B;"><span leaf="">{{步骤标题}}</span></span>
  </section>
  <p style="margin:0;font-size:14px;color:#3E3E3E;line-height:1.75;">
    <span leaf="">{{步骤说明}}</span>
  </p>
</section>
```

---

## 组件 20 流程胶囊 flow-pills

```html
<section style="margin:0 10px 20px;padding:14px 16px;border:1px solid #E5E5E5;border-radius:8px;background:#FAFAFA;">
  <p style="margin:0 0 10px;font-size:11px;font-weight:800;letter-spacing:2px;color:#A0A0A0;"><span leaf="">STUDY FLOW</span></p>
  <section style="display:flex;flex-wrap:wrap;">
    <span style="display:inline-block;padding:5px 10px;border-radius:999px;background:#001E5B;color:#fff;font-size:12px;font-weight:700;margin:0 6px 6px 0;"><span leaf="">{{阶段1}}</span></span>
    <span style="display:inline-block;padding:5px 10px;border-radius:999px;background:#EEF1F8;border:1px solid #D6DCEB;color:#001E5B;font-size:12px;font-weight:700;margin:0 6px 6px 0;"><span leaf="">{{阶段2}}</span></span>
    <span style="display:inline-block;padding:5px 10px;border-radius:999px;background:#F3E8FF;border:1px solid #E9D5FF;color:#5B21B6;font-size:12px;font-weight:700;margin:0 6px 6px 0;"><span leaf="">{{阶段3}}</span></span>
    <span style="display:inline-block;padding:5px 10px;border-radius:999px;background:#69318E;color:#fff;font-size:12px;font-weight:700;margin:0 6px 6px 0;"><span leaf="">{{阶段4}}</span></span>
  </section>
</section>
```

---

## 组件 21 图片卡 image-card

```html
<section style="padding:0 10px;margin-bottom:20px;">
  <section style="border:1px solid #E5E5E5;border-radius:8px;padding:6px;background:#FFFFFF;box-shadow:0 2px 8px rgba(0,30,91,0.06);">
    <span leaf=""><img src="{{图片URL}}" alt="配图" style="max-width:100%;height:auto;display:block;margin:0 auto;border-radius:4px;"></span>
  </section>
  <p style="margin:10px 0 0;font-size:12px;color:#A0A0A0;text-align:center;">
    <span leaf="">— {{图片说明}}</span>
  </p>
</section>
```

无说明时删掉说明 `<p>`。多行代码块用通用库 1a/1b，左竖条换 `#69318E` 或 `#001E5B`。

---

## 组件 22 导航看点三卡 toc-cards

> 精选 3 个核心看点，不是全量目录。

```html
<section style="padding:0 10px 24px;">
  <p style="margin:0 0 12px;font-size:13px;color:#A0A0A0;letter-spacing:1px;"><span leaf="">📌 本文看点</span></p>
  <section style="display:flex;">
    <section style="flex:1;background:#EEF1F8;border:1px solid #D6DCEB;border-radius:8px;padding:14px 10px;margin-right:8px;text-align:center;">
      <p style="margin:0 0 6px;"><span style="display:inline-block;background:#001E5B;color:#fff;font-size:11px;font-weight:800;padding:2px 8px;border-radius:4px;"><span leaf="">01</span></span></p>
      <p style="margin:0;font-size:12px;font-weight:700;color:#001E5B;"><span leaf="">{{看点一}}</span></p>
    </section>
    <section style="flex:1;background:#F5F4F8;border:1px solid #E5E5E5;border-radius:8px;padding:14px 10px;margin-right:8px;text-align:center;">
      <p style="margin:0 0 6px;"><span style="display:inline-block;background:#69318E;color:#fff;font-size:11px;font-weight:800;padding:2px 8px;border-radius:4px;"><span leaf="">02</span></span></p>
      <p style="margin:0;font-size:12px;font-weight:700;color:#001E5B;"><span leaf="">{{看点二}}</span></p>
    </section>
    <section style="flex:1;background:#EEF1F8;border:1px solid #D6DCEB;border-radius:8px;padding:14px 10px;text-align:center;">
      <p style="margin:0 0 6px;"><span style="display:inline-block;background:#001E5B;color:#fff;font-size:11px;font-weight:800;padding:2px 8px;border-radius:4px;"><span leaf="">03</span></span></p>
      <p style="margin:0;font-size:12px;font-weight:700;color:#001E5B;"><span leaf="">{{看点三}}</span></p>
    </section>
  </section>
</section>
```

---

## 组件 23 END 结束线 end-divider

```html
<section style="padding:16px 10px 24px;text-align:center;">
  <section style="display:flex;align-items:center;justify-content:center;">
    <span style="height:1px;width:48px;background:#001E5B;margin-right:12px;"><span leaf=""><br></span></span>
    <span style="font-size:12px;font-weight:800;color:#001E5B;letter-spacing:4px;"><span leaf="">END</span></span>
    <span style="height:1px;width:48px;background:#001E5B;margin-left:12px;"><span leaf=""><br></span></span>
  </section>
</section>
```

---

## 组件 24 文献来源脚注 source-footer

**用途**：参考文末尾【文献来源】/【原文链接】/【发布声明】固定结构。

```html
<section style="margin:0 10px 24px;padding:16px 18px;background:#FAFAFA;border:1px solid #E5E5E5;border-radius:8px;">
  <p style="margin:0 0 8px;font-size:13px;color:#3E3E3E;line-height:1.7;">
    <span style="font-weight:700;color:#001E5B;"><span leaf="">【文献来源】</span></span>
    <span leaf="">：{{期刊与日期}}</span>
  </p>
  <p style="margin:0 0 8px;font-size:13px;color:#3E3E3E;line-height:1.7;">
    <span style="font-weight:700;color:#001E5B;"><span leaf="">【原文链接】</span></span>
    <span leaf="">：{{链接或「见原文」}}</span>
  </p>
  <p style="margin:0;font-size:12px;color:#A0A0A0;line-height:1.7;">
    <span style="font-weight:700;"><span leaf="">【发布声明】</span></span>
    <span leaf="">：{{声明文案，默认：如涉及版权问题，请联系我们及时删除}}</span>
  </p>
</section>
```

---

## 组件 25 术语释义 glossary

```html
<section style="margin:0 10px 20px;padding:14px 16px;background:#FAFAFA;border-radius:8px;border:1px solid #E5E5E5;">
  <p style="margin:0 0 8px;font-size:12px;font-weight:800;color:#69318E;letter-spacing:1px;"><span leaf="">GLOSSARY · 术语</span></p>
  <p style="margin:0 0 6px;font-size:14px;color:#001E5B;font-weight:700;"><span leaf="">{{术语名}}</span></p>
  <p style="margin:0;font-size:13px;color:#5E5E5E;line-height:1.7;"><span leaf="">{{释义}}</span></p>
</section>
```

---

## 组件 26 证据标签行 evidence-tags

```html
<section style="padding:0 20px;margin-bottom:20px;">
  <span style="display:inline-block;background:#001E5B;color:#fff;font-size:11px;font-weight:700;padding:3px 10px;border-radius:4px;margin:0 6px 6px 0;"><span leaf="">{{标签1}}</span></span>
  <span style="display:inline-block;background:#EEF1F8;color:#001E5B;font-size:11px;font-weight:700;padding:3px 10px;border-radius:4px;margin:0 6px 6px 0;border:1px solid #D6DCEB;"><span leaf="">{{标签2}}</span></span>
  <span style="display:inline-block;background:#F3E8FF;color:#5B21B6;font-size:11px;font-weight:700;padding:3px 10px;border-radius:4px;margin:0 6px 6px 0;border:1px solid #E9D5FF;"><span leaf="">{{标签3}}</span></span>
</section>
```

---

## 组件 27 结论收束卡 closing

```html
<section style="margin:8px 10px 24px;background:#001E5B;border-radius:8px;padding:8px;">
  <section style="border:1px solid rgba(255,255,255,0.18);border-radius:6px;padding:18px 20px;">
    <p style="margin:0 0 8px;font-size:10px;font-weight:800;letter-spacing:3px;color:rgba(255,255,255,0.55);"><span leaf="">CLOSING</span></p>
    <p style="margin:0;font-size:15px;font-weight:700;color:#FFFFFF;line-height:1.8;"><span leaf="">{{收束金句}}</span></p>
  </section>
</section>
```

全文 ≤1 处。

---

## 组件 28 签名互动区 signature

```html
<section style="margin:0 10px 24px;padding:20px 16px;border:1px solid #E5E5E5;border-radius:8px;text-align:center;background:#FAFAFA;">
  <p style="margin:0 0 12px;font-size:14px;color:#3E3E3E;line-height:1.7;text-align:justify;">
    <span leaf="">我是 {{作者名}}，{{一句话简介}}。</span>
  </p>
  <p style="margin:0 0 14px;font-size:14px;color:#3E3E3E;line-height:1.7;text-align:justify;">
    <span leaf="">如果这篇文献共读对你有帮助，欢迎</span>
    <strong style="color:#001E5B;"><span leaf="">点赞、在看、转发</span></strong>
    <span leaf="">三连，我们下篇见。</span>
  </p>
  <p style="margin:0;font-size:10px;letter-spacing:2px;color:#A0A0A0;font-weight:600;">
    <span leaf="">THANKS FOR READING</span>
  </p>
</section>
```

原文已有签名则并入此处，不重复。

---

## 组件 29 刊头轻量条 / 深蓝分节条

### 轻量

```html
<section style="margin:0 10px 20px;background:#EEF1F8;border-radius:6px;padding:10px 14px;display:flex;align-items:center;justify-content:space-between;">
  <p style="margin:0;font-size:11px;font-weight:800;letter-spacing:3px;color:#001E5B;"><span leaf="">{{刊头标签}}</span></p>
  <p style="margin:0;font-size:11px;color:#A0A0A0;"><span leaf="">{{右侧说明}}</span></p>
</section>
```

### 深蓝强调（全文 ≤2）

```html
<section style="margin:0 10px 20px;background:#001E5B;border-radius:6px;padding:12px 16px;display:flex;align-items:center;justify-content:space-between;">
  <p style="margin:0;font-size:11px;font-weight:800;letter-spacing:3px;color:#FFFFFF;"><span leaf="">{{刊头标签}}</span></p>
  <p style="margin:0;font-size:11px;color:rgba(255,255,255,0.65);"><span leaf="">{{说明}}</span></p>
</section>
```

---

## 组件 30 重点观点框 key-point

```html
<section style="margin:0 10px 20px;border:1px solid #DBDBDB;border-radius:8px;padding:16px 18px;background:#FFFFFF;">
  <p style="margin:0;font-size:15px;color:#3E3E3E;line-height:1.8;text-align:justify;">
    <span style="font-weight:700;color:#001E5B;border-bottom:3px solid #C4B5FD;"><span leaf="">{{重点观点}}</span></span>
    <span leaf="">　{{补充说明}}</span>
  </p>
</section>
```

---

## 完整文章模板骨架

### A. 文献共读标准骨架（推荐，对齐参考文）

```html
<section style="max-width:677px;margin:0 auto;background:#FFFFFF;font-family:-apple-system,BlinkMacSystemFont,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;color:#3E3E3E;line-height:1.8;letter-spacing:0.5px;overflow-x:hidden;">

  <!-- 1. 系列封面刊头（组件2，可选；平台封面图已有时可省） -->
  <!-- 2. 文献题框卡（组件3） -->
  <!-- 3. 证据标签行（组件26，可选） -->
  <!-- 4. 背景导读（组件4） -->
  <!-- 5. 导航看点（组件22，章节≥3 时） -->
  <!-- 6. 图注 A/B/C（组件5，有解剖/术式图时） -->
  <!-- 7. 重申标题（组件6，可选） -->
  <!-- 8. 双组对照卡（组件15，比较研究时） -->
  <!-- 9. IMRaD：研究目的（组件7 + 组件10 正文） -->
  <!-- 10. IMRaD：研究方法（组件7 + 步骤19/流程20/列表18/正文） -->
  <!-- 11. IMRaD：研究结果（组件7 + 指标16/对照表17/正文） -->
  <!-- 12. IMRaD：研究结论（组件7 + 金句13/收束27） -->
  <!-- 13. 文献摘要（组件12，可选） -->
  <!-- 14. 阅读注意（组件14b，写清限制） -->
  <!-- 15. END（组件23） -->
  <!-- 16. 文献来源脚注（组件24） -->
  <!-- 17. 签名互动（组件28） -->

</section>
```

### B. 通用深度解读骨架

头图/题框 → 导读 → 编号章节 01… → 结论收束 → END → 来源脚注 → 签名。

**骨架铁律**：
- 文献共读类优先用 **IMRaD 组件 7**，不要硬套红白式「01/02 红底编号」除非用户指定。
- **来源脚注（24）在 END 之后、签名之前**；无来源信息时删 24，不要编造期刊名。
- 一篇只有一个 END + 一个签名区。
- 图注 A/B/C 的字母与说明必须与图中标注一致，勿臆造。

---

## 视觉层级（3 层递进）

| 层级 | 样式 | 用途 | 频率 |
|------|------|------|------|
| **锚点层** | 深蓝加粗 11a、结论金句 13、收束卡 27、题框 3 | 核心结论、术式名、PASS/MCID 关键发现 | 全文 ≤5 处深蓝锚点 |
| **标记层** | 淡紫下划线 11d、概念标签 11c | 正文关键词、量表名 | 每段 1~3 处 |
| **容器层** | IMRaD 分节 7、摘要 12、对照/指标 15–17、来源 24 | 结构与数据 | 按需 |

**克制原则**：主色海军只在锚点/分节出现；紫用于题框与次强调；大面积白底 + 灰正文。

---

## 文章类型 → 组件组合配方

| 文章类型 | 核心组件组合 | 点缀组件 |
|---|---|---|
| **文献共读 / 临床研究解读（默认）** | 题框3 + 背景4 + IMRaD7×4 + 正文10 + 来源24 + END23 | 图注ABC5、对照15、指标16、注意14b、摘要12 |
| 指南/共识摘要 | 题框3 + 编号章节8 + 列表18 + 重点观点30 + 来源24 | 术语25、证据标签26 |
| 术式/器械对比 | 题框3 + 对照卡15 + 对照表17 + 步骤19 + 结论13 | 双图（通用）、流程20 |
| 数据复盘/队列结果 | 指标16 + 对照表17 + 结果节7 + 达标14c | 进度类用指标卡代替复杂图表 |
| 病例/个案共读 | 背景4 + 时间线式步骤19 + 金句13 + 来源24 | 图片21、旁注14d |
| 观点/述评（借本主题气质） | 题框3 + 编号8 + 金句13 + 收束27 | 看点22、注意14b |

所有类型共用：END23 +（有来源则）24 + 签名28。

---

## Markdown → 文献共读 映射规则

| Markdown 元素 | 对应组件 | 说明 |
|---|---|---|
| `# 标题` / 文题 | 组件3 题框卡 | 可加「文献共读 \|」前缀 |
| 文首系列名/封面 | 组件2 系列封面 | 可选 |
| 开头背景长段 | 组件4 背景导读 | |
| `## 研究目的/方法/结果/结论` | 组件7 IMRaD 分节 | 优先于通用编号章节 |
| `## 其他章节` | 组件8 编号章节 | |
| `### 子标题` | 组件9 左竖条子节 | |
| 普通段落 | 组件10 + 11d 下划线 | 每段 1~3 关键词 |
| `**加粗**` | 11b 普通 / 11a 深蓝锚点 | 锚点全文 ≤5 |
| `==高亮==` | 11c 浅紫概念标签 | |
| 缩写/量表名 | 11e 术语胶囊 | |
| `> 金句/结论` | 组件13 或 12 摘要 | 视位置 |
| `> 限制/注意` | 组件14b | |
| 两组比较叙述 | 组件15 / 17 | |
| 关键数字 | 组件16 指标卡 | |
| Markdown 表格 | 组件17 flex 对照表 | 不用 layout table 滥用 |
| 有序/无序列表 | 组件18 | |
| 步骤流程 | 组件19 / 20 | |
| `![A/B/C 图](url)` | 组件5 或 21 | 有 A/B/C 说明用 5 |
| `---` | 淡紫渐变线或章节间距 | |
| 文末来源/声明 | 组件24 | 固定结构 |
| 文末 | 组件23 END + 28 签名 | |
| ` ``` code ``` ` | 通用库 1a/1b | 左竖条 `#001E5B` 或 `#69318E` |

---

## 与参考文对齐备忘

参考风格（医疗文献共读栏目）关键视觉转译：

| 参考特征 | 本主题落点 |
|---------|-----------|
| 深蓝「文献共读」封面 | 组件2 `#0A1654` |
| 紫色圆角标题框 | 组件3 `#69318E` 2px 边框 |
| 正文 rgb(62,62,62) | `#3E3E3E` |
| 海军分节/色条 | 组件7 竖条 `#001E5B` |
| A/B/C 图注 | 组件5 |
| 目的/方法/结果/结论 | 组件7 IMRaD |
| END + 来源脚注 | 组件23 + 24 |

> 本主题不绑定任何具体品牌 Logo/商标；系列名与作者由用户替换。
