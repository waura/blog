Title: SwipeRefreshLayoutのsetRefreshing(true)が効かない場合の対処
Date: 2015-11-14 21:46
Author: waura
Category: Android
Tags: Android
Slug: swiperefreshlayout_setrefreshing
Status: published

SwipeRefreshLayoutのsetRefreshing(true)は、onMeasure()が呼ばれるまでは有効にならないみたいです。

参考：<https://code.google.com/p/android/issues/detail?id=77712>

このような場合、SwipeRefreshLayoutを継承して下記のようにsetRefreshingが呼ばれた時の引数の値を覚えておいて、onMesure()のタイミングでsetRefreshing()をもう一回読んであげると良いようです。

```java 
// MySwipeRefreshLayout.java  
public class MySwipeRefreshLayout extends SwipeRefreshLayout {  
  private boolean mMeasured = false;
  private boolean mPreMeasureRefreshing = false;

  public MySwipeRefreshLayout(Context context) {  
    super(context);  
  }

  public MySwipeRefreshLayout(Context context, AttributeSet attrs) {  
    super(context, attrs);  
  }

  @Override  
  public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {  
    super.onMeasure(widthMeasureSpec, heightMeasureSpec);  
    if (!mMeasured) {  
      mMeasured = true;  
      setRefreshing(mPreMeasureRefreshing);  
    }  
  }

  @Override  
  public void setRefreshing(boolean refreshing) {  
    if (mMeasured) {  
      super.setRefreshing(refreshing);  
    } else {  
      mPreMeasureRefreshing = refreshing;  
    }  
  }  
}  
```
