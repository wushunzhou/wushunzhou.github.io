---
title: QUIC协议是如何做到0RTT加密传输
date: 2023-06-06 19:38:21
tags: 随笔
categories: QUIC协议
---

文章参考 [链接地址](https://chengxuyuanwenku.tumblr.com/post/186580241176/%E5%8E%9Fquic%E5%8D%8F%E8%AE%AE%E6%98%AF%E5%A6%82%E4%BD%95%E5%81%9A%E5%88%B00rtt%E5%8A%A0%E5%AF%86%E4%BC%A0%E8%BE%93%E7%9A%84addons)

QUIC作为HTTP2.0形成草案，提上日程以来最重要的(我认为是最重要的，如果你非要说TCP，就当我什么都没说)传输协议，它有很多可以快速秒掉TCP的特质，本文来介绍其中一个，即0RTT。