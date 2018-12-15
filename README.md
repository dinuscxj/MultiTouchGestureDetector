
## MultiTouchGestureDetector
[中文版文档](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/README-ZH.md)&nbsp;&nbsp;&nbsp;

![](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/Preview/gesture.jpg)

The [MultiTouchGestureDetector](https://github.com/dinuscxj/MultiTouchGestureDetector) Detects scaling, rotating and moving transformation gestures
using the supplied `MotionEvent`s. The `OnMultiTouchGestureListener` callback will notify users when a particular gesture event has occurred,
besides, ` SimpleOnMultiTouchGestureListener` is offered as a helper class that you can extend if you don’t care about all of the reported events.
This class should only be used with `MotionEvent`s reported via touch.

![](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/Preview/MultiTouchGestureDetector.gif?width=300)

### Usage
Step 1. Create our `MultiTouchGestureDetector`
```java
        mMultiTouchGestureDetector = new MultiTouchGestureDetector(context, new MultiTouchGestureDetectorListener());
```

Step 2. Let the `MultiTouchGestureDetector` inspect all events.
```java
        mMultiTouchGestureDetector.onTouchEvent(event);
```

Step 3. Record the detected gesture transformations.
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

Step 4. Apply the gesture transformations
```java
        canvas.save();
        canvas.translate(mOffsetX, mOffsetY);
        canvas.scale(mScaleFactor, mScaleFactor, mIcon.getIntrinsicWidth() / 2, mIcon.getIntrinsicHeight() / 2);
        canvas.rotate(mRotation, mIcon.getIntrinsicWidth() / 2, mIcon.getIntrinsicHeight() / 2);
        mIcon.draw(canvas);
        canvas.restore();

```

If necessary the full usage is [here](https://github.com/dinuscxj/MultiTouchGestureDetector/blob/master/MultiTouchGestureDetector/app/src/main/java/com/dinuscxj/gesturedetector/demo/MultiTouchGestureView.java).

#### Gradle
```gradle
    dependencies {
        compile 'com.dinuscxj:multitouchgesturedetector:1.0.0'
    }
```

#### Application scenarios
* Sticker system. such as the story feature of the Instagram.
* Media Browsing. such as the feed detail page of the Facebook

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
