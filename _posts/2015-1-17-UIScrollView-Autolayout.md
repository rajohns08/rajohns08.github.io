---
layout: post
title: Setting up a UIScrollView with Auto Layout in iOS
---

When setting up a UIScrollView using Auto Layout, there were a couple of tricky things that tripped me up the first time I attempted it. My personal litmus test for determining if I have set up a proper UIScrollView is making sure a UILabel word wraps correctly, so that is why I will be using a UILabel in this guide. Here are the steps I take now to set up a UIScrollView:


1. Assuming you are starting with a blank UIViewController in Storyboard, drag on a UIScrollView:

![_config.yml]({{ site.baseurl }}/images/UIScrollView/1.png)
