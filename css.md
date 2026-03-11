# CSS

### Q : What is diff between display: none and visibility: hidden?  
A : 
**display: none**

* Element **completely removed** from page
* **No space** is kept
* Other elements **move up**

Example:
```css
display: none;
```

Result:
```
Before:  [Box1] [Box2]
After :  [Box2]
```
---
**visibility: hidden**

* Element **not visible**
* **Space is still kept**
* Layout **does not change**

Example:
```css
visibility: hidden;
```
Result:
```
Before:  [Box1] [Box2]
After :  [     ] [Box2]
```
---
**Quick difference**
|                | display:none | visibility:hidden |
| -------------- | ------------ | ----------------- |
| Visible        | ❌            | ❌                 |
| Space kept     | ❌            | ✅                 |
| Layout changes | ✅            | ❌                 |

✅ **Easy trick**

* `display:none` → remove element
* `visibility:hidden` → hide element but keep space


### Q: Difference between `position: relative` and `position: absolute`

**position: relative**

* Element stays in **normal layout**
* Moves **relative to its own position**
* **Space is still kept**

Example:
```css
.box {
  position: relative;
  top: 10px;
  left: 10px;
}
```
Result:
Element moves slightly, but its **original space remains**.

---

**position: absolute**
* Element **removed from normal layout**
* Positioned **relative to nearest positioned parent**
* **No space is kept**

Example:
```css
.box {
  position: absolute;
  top: 10px;
  left: 10px;
}
```
Result:
Element moves and **other elements ignore its space**.

---

**Quick difference**

|                      | relative      | absolute                  |
| -------------------- | ------------- | ------------------------- |
| Layout flow          | stays in flow | removed from flow         |
| Space kept           | ✅             | ❌                         |
| Position relative to | itself        | nearest positioned parent |

✅ **Easy trick**

* `relative` → move **relative to itself**
* `absolute` → move **relative to parent**
