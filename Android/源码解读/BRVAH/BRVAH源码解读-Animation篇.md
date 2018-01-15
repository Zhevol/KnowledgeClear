### BRVAH 源码解读 - Animation篇

#### 一、Animation 篇概要

　　Animation 篇主要关注 BRVAH 的源码中的 animation 包下的类。该包中，包含了接口类 BaseAnimation 和五个实现类 AlphaInAnimation、ScaleInAnimation、SlideInBottomAnimation、SlideInLeftAnimation、SlideInRightAnimation。

#### 二、 BaseAnimation 类

　　BaseAnimation 类是一个接口方法类，定义了一个方法 `getAnimators()` 传递一个参数 View，返回值为 Animator 的数组。

#### 三、AlphaInAnimation 类

　　从字面意义上理解，此类是渐变进入的动画。其源代码如下：

```
    public class AlphaInAnimation implements BaseAnimation {
        private static final float DEFAULT_ALPHA_FROM = 0f;
        private final float mFrom;

        public AlphaInAnimation() {
            this(DEFAULT_ALPHA_FROM);
        }

        public AlphaInAnimation(float from) {
        mFrom = from;
        }

        @Override
        public Animator[] getAnimators(View view) {
            return new Animator[]{ObjectAnimator.ofFloat(view, "alpha", mFrom, 1f)};
        }
    }
```

　　从以上代码知道，此类是 BaseAnimation 类的实现类。渐变进入的动画，其默认的起始透明度值为0，类中定义了两个构造函数，一为默认的构造器，二为带透明度的构造器。当调用默认构造器的时候，使用默认的透明度值；当使用带透明度的构造器的时候，需要传递一个透明度参数。然后在 `getAnimators()` 方法中，返回一个动画的数组。用于改变控件的透明度属性从 `mFrom` 值变化到不透明。

　　使用该动画的效果如下：

　　![AlphaInAnimation 效果](/pictures/渐变进入动画.gif)

#### 四、ScaleInAnimation 类

　　该类定义了缩放进入的动画，其源代码如下：

```
    public class ScaleInAnimation implements BaseAnimation {
        private static final float DEFAULT_SCALE_FROM = .5f;
        private final float mFrom;

        public ScaleInAnimation() {
            this(DEFAULT_SCALE_FROM);
        }

        public ScaleInAnimation(float from) {
            mFrom = from;
        }

        @Override
        public Animator[] getAnimators(View view) {
            ObjectAnimator scaleX = ObjectAnimator.ofFloat(view, "scaleX", mFrom, 1f);
            ObjectAnimator scaleY = ObjectAnimator.ofFloat(view, "scaleY", mFrom, 1f);
            return new ObjectAnimator[]{scaleX, scaleY};
        }
    }
```

　　首先，定义一个默认的缩放起始值 `DEFAULT_SCALE_FROM` 为0.5，也就是控件 View 的一半大小。当外部使用的时候，如果想改变起始的缩放大小，只需要调用形参构造器并传递缩放的参数，就可以改变 `mFrom` 的值，该值用于在 `getAnimators()` 中返回动画数组。如果只需要使用默认的缩放大小，调用无参构造器即可。在 `getAnimators()` 的方法中，将控件 View 从X和Y两个方向上同时对控件进行缩放，最终返回了包含缩放动画的数组。

　　使用该动画的效果如下：

　　![ScaleInAnimation 效果](/pictures/缩放进入动画.gif)

#### 五、SlideInBottomAnimation 类

　　该类定义了从底部滑动进入的动画，其源码如下：

```
    public class SlideInBottomAnimation implements BaseAnimation {
        @Override
        public Animator[] getAnimators(View view) {
            return new Animator[]{
                    ObjectAnimator.ofFloat(view, "translationY", view.getMeasuredHeight(), 0)
            };
        }
    }
```

　　直接让 View 从Y坐标的测量的高度的位置，滑动到对应坐标为0的位置。注意这里的0所在的坐标系不是 RecyclerView 的坐标系，而是单独的一个子 View 的坐标系。

　　使用该动画的效果如下：

　　![SlideInBottomAnimation 效果](/pictures/底部滑动进入动画.gif)

#### 六、SlideInLeftAnimation 类

　　该类定义了从左边滑动进入的动画，其源码如下：

```
    public class SlideInLeftAnimation implements BaseAnimation {
        @Override
        public Animator[] getAnimators(View view) {
            return new Animator[]{
                    ObjectAnimator.ofFloat(view, "translationX", -view.getRootView().getWidth(), 0)
            };
        }
    }
```

　　直接让 View 从其根视图的宽度的相反值处的X坐标，滑动到X坐标为0的位置。注意此坐标系是相对于子 View 的坐标系，不是 RecyclerView 的坐标系。

　　使用该动画的效果如下：

　　![SlideInBottomAnimation 效果](/pictures/左边滑动进入动画.gif)

#### 七、SlideInRightAnimation 类

　　该类定义了从右边滑动进入的动画，其源码如下：

```
    public class SlideInRightAnimation implements BaseAnimation {
        @Override
        public Animator[] getAnimators(View view) {
            return new Animator[]{
                    ObjectAnimator.ofFloat(view, "translationX", view.getRootView().getWidth(), 0)
            };
        }
    }
```

　　直接让 View 从其根视图的宽度的处的X坐标，滑动到X坐标为0的位置。这里的坐标系依然是子 View 的坐标系。

　　使用该动画的效果如下：

　　![SlideInBottomAnimation 效果](/pictures/右边滑动进入动画.gif)

#### 八、自定义动画

　　同样的，如果要实现提供的以上五种动画之外的动画，就需要自定义动画了。以下是其中的一种自定义动画：

```
    public class CustomAnimation implements BaseAnimation {

        @Override
        public Animator[] getAnimators(View view) {
            return new Animator[]{
                   ObjectAnimator.ofFloat(view, "scaleY", 1, 1.1f, 1),
                   ObjectAnimator.ofFloat(view, "scaleX", 1, 1.1f, 1)
            };
        }
    }
```

　　该动画定义的仍然是缩放动画，但其变现形式是先放大一点再还原。

　　使用该动画的效果如下：

　　![SlideInBottomAnimation 效果](/pictures/自定义进入动画.gif)