# wcskill

Ounin 的内容创作工具箱。做成 Claude Code skill，给创作者用。

---

## 工具箱


| Skill           | 做什么                           |
| --------------- | ----------------------------- |
| `/wc`           | 主入口，自动路由到对的工具                 |
| `/wc-xhs-title` | 小红书标题引擎。从 62 套验证过的标题结构中匹配最优方案 |


---

## 安装

```bash
git clone https://github.com/yx4724201000subf/wcskill.git /tmp/wcskill && cp -r /tmp/wcskill/skills/wc* ~/.claude/skills/ && rm -rf /tmp/wcskill
```

安装后在 Claude Code 中输入 `/wc` 即可。

---

## 使用

```
/wc              → 主入口，告诉你该用哪个工具
/wc-xhs-title   → 直接进入小红书标题引擎
```

### 小红书标题引擎

给一个话题，从 62 套标题结构中自动匹配最合适的 5-8 个，生成定制标题。

- 10 类心理驱动力覆盖（量化锚点、经历叙事、风险警示、反直觉、结果导向、人群锁定、信息差、观点表达、场景互动、权威嫁接）
- 每个标题附结构编号和选用理由
- 输出 Top 3 推荐

---

## 许可证

本项目采用 [MIT License](LICENSE)。