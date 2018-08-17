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
