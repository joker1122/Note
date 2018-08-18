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
# canva绘制Text
* drawText(String text, float x, float y, Paint paint)
> 1. text 是文字内容，x 和 y 是文字的坐标。但需要注意：这个坐标并不是文字的左上角，而是一个与左下角比较接近的位置.

- drawTextOnPath(String text, Path path, float hOffset, float vOffset, Paint paint)
> 1. drawTextOnPath() 使用的 Path ，拐弯处全用圆角，别用尖角。
> 2. hOffset 和 vOffset。它们是文字相对于 Path 的水平偏移量和竖直偏移量，利用它们可以调整文字的位置。例如你设置 hOffset 为 5， vOffset 为 10，文字就会右移 5 像素和下移 10 像素。
* 使绘制的文本支持换行 ***StaticLayout***
> StaticLayout 并不是一个 View 或者 ViewGroup ，而是 android.text.Layout 的子类，它是纯粹用来绘制文字的。StaticLayout 支持换行，它既可以为文字设置宽度上限来让文字自动换行，也会在 \n 处主动换行。
```java
String text1 = "Lorem Ipsum is simply dummy text of the printing and typesetting industry.";
StaticLayout staticLayout1 = new StaticLayout(text1, paint, 600,
        Layout.Alignment.ALIGN_NORMAL, 1, 0, true);
String text2 = "a\nbc\ndefghi\njklm\nnopqrst\nuvwx\nyz";
StaticLayout staticLayout2 = new StaticLayout(text2, paint, 600,
        Layout.Alignment.ALIGN_NORMAL, 1, 0, true);

...

canvas.save();
canvas.translate(50, 100);
staticLayout1.draw(canvas);
canvas.translate(0, 200);
staticLayout2.draw(canvas);
canvas.restore();
```
