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
> 1. text 是文字内容，x 和 y 是文字的坐标。但需要注意：这个坐标并不是文字的左上角，而是一个与左下角比较接近的位置.

- drawTextOnPath(String text, Path path, float hOffset, float vOffset, Paint paint)
> 1. drawTextOnPath() 使用的 Path ，拐弯处全用圆角，别用尖角。
> 2. hOffset 和 vOffset。它们是文字相对于 Path 的水平偏移量和竖直偏移量，利用它们可以调整文字的位置。例如你设置 hOffset 为 5， vOffset 为 10，文字就会右移 5 像素和下移 10 像素。
