### 通过代码设置控件的 `layout_weight` 属性

```
    View view = new View(this);
    LinearLayoutCompat.LayoutParams layoutParams = new LinearLayoutCompat.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, 0, 1.0f);
    view.setLayoutParams(layoutParams);
```

注：其中 `LayoutParams` 的第一个属性为宽的设置、第二个属性为高的设置，第三个属性就是 `weight` 属性的设置。