---
title: flex box vs grid layout in implementation of image card
date: 2018-03-28 08:52:15
tags:
---

Html element layout process seems to be simple for a trained coder, the same as a skilled front-end coder, just a piece of cake. But the fact is that even to me, working with javascript/html/css for many years occasionally lost in how to center an image with equal margin.

Below is a mini-program image card, constructed by view and css, it consumed me couples of hour to complete it.... **-_-||** ... It's so frustrated that I begin to doubt I'm too old to do this....

![](/img/image_card.png)

the view structure is simple:

```
<!-- image header card -->
<view class="card">
  <view class="image-roundcorner">
    <image class="header-img shadow" src="../../images/card_header_img1.png"></image>
  </view>
  <view class="footer ">
    <view class="footer-title">揭秘区块链系列</view>
    <view class="footer-tags shadow">
      <text class="tag">创新科技</text>
      <text class="tag">创新科技</text>
      <text class="tag">创新科技</text>
    </view>
  </view>
</view>

```

The card class define the card's size merely, 100% width and 255px height. The most confusing part is centering the header image and leave the left and the right equal margin to screen border. I had thought that just having the image container 100% with and margin: 0 10px would realize the expectation. But it turned out I'm thinking too easy. The working design ending up in this:

```
.card .image-roundcorner {
  width: 100%;
  height: 150px;

  /* image container just define a center-ability box */
  display: flex;
  justify-content: center;
}

.card .header-img {
  width: 100%;
  height: 100%;

  /* importantly place here to determine center & LR margin */
  margin: 0 10px;

  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  overflow: hidden;
}

```

As for footer, to center two row text and leave equal margin, **flex-direction** is a must:

```
.card .footer {
  width: 100%;
  height: auto;

  display: flex;
  justify-content: center;

  /* vertically arrange the children */
  flex-direction: column;
}
```

All this layout details and small techniques are not difficult or tricky for a skilled front-end coder writing them daily, but could drive someone unfamiliar  about this crazy.

Finally I compared the flex box layout method with grid layout, the result showed that css grid can greatly cut down the code amount(~10% saved), the view structure simplified as well:

```
<!-- optimized image header card -->
<view class="grid-card">
  <image class="header-img" src="../../images/card_header_img2.png"></image>
  <text class="footer-title">谈创新你必须知道这些</text>
  <view class="footer-tags shadow">
    <text class="tag">创新科技</text>
    <text class="tag">创新科技</text>
    <text class="tag">创新科技</text>
  </view>
</view>

```

2 view container reduced thanks for display: grid;

- first define a grid card structure with column and row:
```
.grid-card {
  width: 100%;
  height: 255px;

  display: grid;
  grid-template-columns: 10px auto 10px;
  grid-template-rows: 150px 42px 46px;
}

```

- then just put the element in it directly :
```
.grid-card .header-img {
  grid-column: 2/3;
  grid-row: 1/2;

  width: 100%;
  height: 150px;

  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  overflow: hidden;
}

```

The total layout process are clear and under the control, it's a big advance compared with flex box layout. So, it's time to leap toward to css grid layout age.


...
