---
layout: post
title: "Smooth scrolling for HorizontalScrollView"
date: 2013-03-22 14:23
comments: true
categories: 
published: false
---

Just something related to the HorizontalScrollView we worked on last summer. Remember we had a problem getting it to scroll smoothly through smoothscrollTo? I tried implementing a similar HorizontalScrollView and I think the problem is because the Scroller in HorizontalScrollView is private (so is the smoothScrollTo function). The current Scroller implemented uses a linear interpolator which ends the animation abruptly. In order to get past that, I made a ghost scroller with a custom interpolator I(t) = (t-1)^5 + 1 (I got this from the Prixing app) and have a runnable that updates the scroll position of the HorizontalScrollView based on the ghost scroller.

<!-- more -->

[Cyril Mottier's article](http://cyrilmottier.com/2012/05/22/the-making-of-prixing-fly-in-app-menu-part-1/) about Prixing's Fly-in App Menu

``` java Using SmoothScrollTo
public void open(){
    smoothScrollTo(openedX, 0);
    ((Activity) this.getContext()).getActionBar().setDisplayHomeAsUpEnabled(false);
}
```


``` java Implementation using ghost scroller
public void open(){
    mScroller.startScroll(getScrollX(), 0, openedX - getScrollX(), 0, 500);
    post(scrollerTask);
//      smoothScrollTo(openedX, 0);
    ((Activity) this.getContext()).getActionBar().setDisplayHomeAsUpEnabled(false);
}

public Runnable scrollerTask = new Runnable() {
    @Override
    public void run() {
        mScroller.computeScrollOffset();
        scrollTo(mScroller.getCurrX(), 0);

        if (!mScroller.isFinished()) {
            ScrollView.this.post(this);
        }
    }
};
```

// Need logic here to stop runnable if touch is detected during animation
onTouch