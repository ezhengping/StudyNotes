# 标题样式

``` markdown
# 这是 <h1> 一级标题
## 这是 <h2> 二级标题
### 这是 <h3> 三级标题
#### 这是 <h4> 四级标题
##### 这是 <h5> 五级标题
###### 这是 <h6> 六级标题
```
如果你想要给你的标题添加 `id` 或者 `class`，请在标题最后添加 `{#id .class1 .class2}`。例如：

```markdown
# 这个标题拥有 1 个 id {#my_id}
# 这个标题有 2 个 classes {.class1 .class2}
```
# 强调
```markdown
*这会是 斜体的文字*
_这会是 斜体的文字_

**这会是 粗体 的文字**
__这会是 粗体 的文字__

_你也 **组合** 这些符号_

~~这个文字将会被横线删除~~
```

# 列表
### 无序列表
```markdown
* Item 1
* Item 2
  * Item 2a
  * Item 2b
```

### 有序列表
```markdown
1. Item1
2. Item2
3. Item3
   1. Item 3.1
   2. Item 3.2
```


# 添加图片
![images](https://avatars3.githubusercontent.com/u/31007334?s=40&v=4)
```markdown
![images](https://avatars3.githubusercontent.com/u/31007334?s=40&v=4)
Format: ![Alt Text](https://avatars3.githubusercontent.com/u/31007334?s=40&v=4)
```

# 引用
```markdown
正如 Kanye West 所说：

> We're living the future so
> the present is our past.
```


# 分割线
```markdown 
如下，三个或者更多的

---

连字符

***

星号

___

下划线

```

```javascript {.line-numbers}
function add(x, y) {
  return x + y
}
```