
## MultiTouchGestureDetector
[MultiTouchGestureDetector](https://github.com/dinuscxj/MultiTouchGestureDetector) 通过提供的`MotionEvent`
统一处理缩放、旋转、移动手势变换。 当任何一个可察觉的手势发生变化，`OnMultiTouchGestureListener` 回调将会被触发，
此外`SimpleOnMultiTouchGestureListener` 是一个辅助类， 如果你不需要关心所有回调事件的话，可以优先继承它。
这个类一定要注入View的触摸事件。

![](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/Preview/MultiTouchGestureDetector.gif?width=300)

### Usage
Step 1. 创建 `MultiTouchGestureDetector`
```java
        mMultiTouchGestureDetector = new MultiTouchGestureDetector(context, new MultiTouchGestureDetectorListener());
```

Step 2. `MultiTouchGestureDetector` 监听触摸 Event
```java
        mMultiTouchGestureDetector.onTouchEvent(event);
```

Step 3. 记录手势变换的结果
```java
private final class MultiTouchGestureDetectorListener extends MultiTouchGestureDetector.SimpleOnMultiTouchGestureListener {

        @Override
        public void onScale(MultiTouchGestureDetector detector) {
            mScaleFactor *= detector.getScale();
            mScaleFactor = Math.max(1.0f, Math.min(mScaleFactor, 5.0f));

            invalidate();
        }

        @Override
        public void onMove(MultiTouchGestureDetector detector) {
            mOffsetX += detector.getMoveX();
            mOffsetY += detector.getMoveY();

            invalidate();
        }

        @Override
        public void onRotate(MultiTouchGestureDetector detector) {
            mRotation += detector.getRotation();

            invalidate();
        }
    }
```

Step 4. 应用手势变换
```java
        canvas.save();
        canvas.translate(mOffsetX, mOffsetY);
        canvas.scale(mScaleFactor, mScaleFactor, mIcon.getIntrinsicWidth() / 2, mIcon.getIntrinsicHeight() / 2);
        canvas.rotate(mRotation, mIcon.getIntrinsicWidth() / 2, mIcon.getIntrinsicHeight() / 2);
        mIcon.draw(canvas);
        canvas.restore();

```

如果想查看全部使用方法，可以点击 [这里](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/MultiTouchGestureDetector/app/src/main/java/com/dinuscxj/gesturedetector/demo/MultiTouchGestureView.java).

#### Gradle
```gradle
    dependencies {
        compile 'com.dinuscxj:multitouchgesturedetector:1.0.0'
    }
```

#### 使用场景
* 贴纸系统，比如Instagram的story 功能.
* 媒体浏览系统， 比如facebook 的详情页。

### License
    Copyright 2015-2019 dinuscxj

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
