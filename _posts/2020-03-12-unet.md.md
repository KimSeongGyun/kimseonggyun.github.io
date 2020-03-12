---
title: "[논문구현] U-net:Convolutional Networks for Biomedical Image Segmentation"
date: 2020-03-12 23:29:28 -0400
categories: Paper Study
---

오늘 다른 논문은 2015년 발표된 [U-net: Convolutional Networks for Biomedical Image Segmentation](https://arxiv.org/abs/1505.04597) 입니다. 

이전까지의 Convolutional Networks는 주로 하나의 Image 전체에 대해 하나의 Class를 부여하는 Classification 문제를 푸는데 주로 쓰였습니다. 하지만 Medical Image를 처리할 때에는 Image의 각 pixel마다 Class를 부여할 필요가 생겼고, 이를 위해 새롭게 구현된 구조가 U-net입니다. 우선 U-net의 구조를 간단히 살펴보겠습니다.

![](https://user-images.githubusercontent.com/38622987/76529070-1ad13d80-64b5-11ea-8280-41b50820acc3.png)

U-net은 크게 왼쪽의 Contracting Path와 오른쪽의 Expansive Path로 이루어져 있습니다.

Contraction Path에서는 3x3 Convolution 연산과 Resolution을 줄이는 2x2 Maxpooling이 반복적으로 일어나고 Expansive Path에서는 3x3 Convolution 연산과 줄어든 Resolution을 다시 높이기 위한 2x2 UpConvolution(Transposed Convolution)을 합니다.

이때 Contraction Path의 Feature Channel을 Copy&Crop해서 Expansive Path의 Feature Channel에 붙여주는데 상대적으로 high resolution feature에 대한 정보를 전달해주어 Localize를 도와주는 효과를 거둘 수 있습니다.

이 네트워크는 Contracting Path와 Expansive Path가 거의 비슷하게 많은 개수의 Feature Channel를 가지고 대칭적으로 구성되어 있기 때문에 고해상도의 Layer에 Context Information를 전파할 수 있습니다. 
