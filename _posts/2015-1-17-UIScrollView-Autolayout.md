---
layout: post
title: Setting up a UIScrollView with Auto Layout in iOS
---

When setting up a UIScrollView using Auto Layout, there were a couple of tricky things that tripped me up the first time I attempted it. My personal litmus test for determining if I have set up a proper UIScrollView is making sure a UILabel word wraps correctly, so that is why I will be using a UILabel in this guide. Here are the steps I take now to set up a UIScrollView:

1. Assuming you are starting with a blank UIViewController in Storyboard, drag on a UIScrollView:

  ![_config.yml]({{ site.baseurl }}/images/UIScrollView/1.png)

2. Set the leading/top/trailing/bottom constraints to 0 on the UIScrollView. Make sure "Constrain to margins" is NOT checked.

  ![_config.yml]({{ site.baseurl }}/images/UIScrollView/2.png)

3. Drag on a UIView to be a subview of your UIScrollView. This is the key piece of the puzzle that tripped me up for a while. We want all of our elements to be contained in this container UIView inside the UIScrollView.

  ![_config.yml]({{ site.baseurl }}/images/UIScrollView/3.png)

4. Set the leading/top/trailing/bottom constraints to 0 on the UIView. Again, make sure "Constrain to margins" is NOT checked.

5. Make your UIScrollView and UIView have equal widths by Ctrl-dragging from one to the other.

  ![_config.yml]({{ site.baseurl }}/images/UIScrollView/4.png)
