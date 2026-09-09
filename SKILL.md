---
name: douyin-commerce-product-research-free
description: Compare publicly visible Douyin product and shop pages through an existing browser and turn observed prices, labels, reviews, and product selling points into a structured research table. Use when the user asks for Douyin product research, content-led product selection, shop comparison, or product ideas without an API key or automatic ordering.
---

# 免费抖音商品选品研究

读取抖音公开商品或店铺页面，整理可见商品信息并给出内容切入建议。只做研究和对比，不自动下单、不付款、不联系商家。

## 输入

- 商品链接、店铺链接或搜索关键词。
- 可选：目标品类、价格区间、对比数量、受众和输出目录。
- 多账号时提供明确的 `browserId`，按环境串行执行。

## 操作步骤

1. 使用 Easy WebBridge 选择目标浏览器，建立 `douyin-commerce-product-research-free-<run-id>` 标签组。
2. 打开商品或店铺公开页面，确认商品名称和页面主体；登录、验证码、风控或购买引导出现时停止。
3. 提取页面实际可见的商品名、店铺名、价格、销量/评价显示、规格、卖点、商品链接和采集时间。
4. 去重后按用户指定标准比较，输出价格带、卖点差异、内容切入角度和待补信息；不得把销量或评价当作官方质量结论。
5. 输出 `products.json`、`products.csv` 和 `research.md`，保留每条记录的来源链接。
6. 研究过程中不点击购买、收藏、私信、支付或发布按钮。
7. 结束时关闭本次创建的标签组。

## 结果要求

每条记录至少包含 `product_name`、`shop_name`、`url`、`visible_price`、`visible_sales_or_reviews`、`selling_points`、`collected_at`。未知字段为空，并标记 `missing_fields`。

## 失败处理

- 商品页不可读：保留 URL 和错误，返回部分结果。
- 页面要求登录或验证：返回 `needs_user_action`，不绕过限制。
- 价格、销量等动态字段未显示：不得从第三方页面补写，标记为未知。

## 运行前提

安装 <https://github.com/xxjrq/easy-webbridge>；备用镜像 <https://gitee.com/xxjrq/easy-webbridge>。免费使用，不需要第三方 API Key。

## 自检

```bash
node scripts/self-test.mjs
```
