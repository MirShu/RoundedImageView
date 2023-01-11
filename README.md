# RoundedImageView

很多Android app 都会有那种头像重叠横向或者垂直的效果，刚好自己项目也有这需求试试效果。
先看看效果吧！

![2781551-7d767328d069d6ee](https://user-images.githubusercontent.com/13359093/211714873-6bc1b4d8-e38c-4ccd-9e3d-90601dfdc329.png)

我的做法很low 但是也很简单，不知道大家有没有想象的到我用的哪种方法做的呢，

# 第一步

RecyclerView列表数据应该都不用说了吧

是的没错首先看它是个列表就用万能RecyclerView横向展示就是了，是的就是用的它然后item用 android:layout_marginStart="-10dp" 属性去设置重叠,下面的是RecyclerView item

布局文件

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/relayout"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="-10dp"
    android:orientation="vertical">

    <com.makeramen.roundedimageview.RoundedImageView
        android:id="@+id/user_photo"
        android:layout_width="28dp"
        android:layout_height="28dp"
        android:src="@mipmap/icon_default_head_image"
        app:riv_border_color="@color/color_f4f4f4"
        app:riv_border_width="2dp"
        app:riv_corner_radius="60dip"
        app:riv_mutate_background="true"
        app:riv_oval="false" />

    <cn.exmp.app.widget.xscrollview.RoundImageView
        android:id="@+id/iv_rund_more"
        android:layout_width="28dp"
        android:layout_height="28dp"
        android:layout_gravity="center_horizontal"
        android:layout_marginStart="20dp"
        android:scrollbars="none"
        android:src="@mipmap/icon_same_more"
        android:visibility="gone" />
</RelativeLayout>

```

# 第二步：

如果代码不做稍微设置的话，就用android:layout_marginStart="-10dp" 这个属性会出现第一个item左边缺口，所有在代码再设置下setMarginEnd(0);


```
 try {
                    LinearLayout.LayoutParams lp = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.WRAP_CONTENT, LinearLayout.LayoutParams.WRAP_CONTENT);
                    if (position == numberStudentsList.size() - 1) {
                        ivRundMore.setVisibility(View.VISIBLE);
                        lp.setMarginEnd(0);
                    } else {
                        ivRundMore.setVisibility(View.GONE);
                        lp.setMarginEnd(-20);
                    }
                    relayout.setLayoutParams(lp);

                } catch (Exception e) {

                }

```

# 最后 不光左重叠 layout_marginStart="-10dp" 右重叠 android:layout_marginEnd="-10dp"上下重叠 就不用多说了。


虽然方法很一般很low，但是很实用，通俗简单的不能再简单。
