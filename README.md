# Android 属性动画
***做 translation 平移动画是以自身为原点***
```java

public void setAnimator(View correct, View next) {
        setDefault(next);
        mAnimatorSet.playTogether(
                ObjectAnimator.ofFloat(correct, "translationX",
                        0,
                        ChangeUnits.change(correct.getContext(), -correct.getWidth()))
                , ObjectAnimator.ofFloat(correct, "rotationY", 180, 90)
        );
    }
```
## canva绘制Text
* drawText(String text, float x, float y, Paint paint)
>text 是文字内容，x 和 y 是文字的坐标。
但需要注意：这个坐标并不是文字的左上角，而是一个与左下角比较接近的位置。大概在这里：
