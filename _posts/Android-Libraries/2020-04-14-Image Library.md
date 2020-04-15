---
layout: post
title:  Image libraries
categories: Android-Libraries
comments: true
---

### Image Library<br>

<strong><font color="Red">① Glide library</font></strong> <br>

(1) dependencies 추가하기<br>

    //Glide library
    def glideVersion = '4.11.0'
    implementation "com.github.bumptech.glide:glide:$glideVersion"
    // Glide v4 uses this new annotation processor
    annotationProcessor "com.github.bumptech.glide:compiler:$glideVersion"

(2) ImageView에 보여줄 이미지를 binding하는 부분에서 아래와 같이 Glide 라이브러리로 바인딩해준다.<br>
<strong><font color="Blue">[Basic Usage]</font></strong><br>

    // Set the image
    RequestOptions defaultOptions = new RequestOptions()
                                    .error(R.drawable.ic_launcher_background);
    Glide.with(mContext)
                .setDefaultRequestOptions(defaultOptions)
                .load(mNicePlaces.get(position).getImageUrl())
                .into(((Holder)holder).mImage);



### 전체적인 학습내용을 복습한다.<br>
1.
