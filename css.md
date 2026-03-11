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
