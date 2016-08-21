---
layout: post
title: android_layout笔记
tags:
---

##orientation:
	vertical:垂直布局
	horizontal:水平布局（默认）   
##weight：
	权重是按比例分配空间
	当layout_width = wrap_content时按比例分配
	当layout_width = match_parent或fill_parent时
	若记屏幕死长度为x，则a控件需要x，b控件需要x，c控件需要x
	a，b，c权重为1，2，2  
	那么屏幕剩余空间为x - 3x = -2x
	a控件按权重得到的空间为 x + （-2x）* 1/5 = 3/5 * x
	b控件按权重得到的空间为 x + （-2x）* 2/5 = 1/5 * x 
	c控件按权重得到的空间为 x + （-2x）* 2/5 = 1/5 * x
##margin
    layout_margin: 指定布局文件外边距(top left right bottom)
    android:layout_marginTop=""    上边距
    android:layout_marginBottom="" 下边距
    android:layout_marginLeft=""   左边距
    android:layout_marginRight=""  右边距
    
    android:padding:指定内边距(布局文件与控件之间的距离)
    android:paddingLeft="5dp"  指定左内边距
    android:paddingTop="10dp"  指定上内边距
    android:paddingRight="15dp" 指定右内边距
    android:paddingButtom="15dp" 指定下内边距
    
    android:layout_gravity:相对于父控件的对齐方式
    android:gravity="center":控件内容及子控件的对齐方式(View本身)
###android:layout_above  
	将该控件的底部至于给定ID的控件之上,但不会左对齐，默认置于父窗口最左边，会覆盖最左边的控件   
###android:layout_below   
	将该控件的顶部至于给定ID的控件之下,但不会左对齐，默认置于父窗口最左边，会覆盖最左边的控件   
###android:layout_toLeftOf   
	将该控件的右边缘和给定ID的控件的左边缘对齐，默认置于父窗口最上面，会覆盖最上面的控件       
###android:layout_toRightOf  
	将该控件的左边缘和给定ID的控件的右边缘对齐，默认置于父窗口最上面，会覆盖最上面的控件
###android:alignParentBottom   
	如果该值为true，则将该控件的底部和父控件的底部对齐，默认置于父窗口最左下，会覆盖最左下的控件   
###android:layout_alignParentLeft   
	如果该值为true，则将该控件的左边与父控件的左边对齐，默认置于父窗口最左上，会覆盖最左上的控件  
###android:layout_alignParentRight   
	如果该值为true，则将该控件的右边与父控件的右边对齐，默认置于父窗口最右上，会覆盖最右上的控件   
###android:layout_alignParentTop   
	如果该值为true，则将控件的顶部与父控件的顶部对齐，默认置于父窗口最左上，会覆盖最左上的控件
###android:layout_alignBaseline  
	该控件的baseline和给定ID的控件的baseline对齐，并置于父窗口最左边，会覆盖最左边的控件   
###android:layout_alignBottom   
	将该控件的底部边缘与给定ID控件的底部边缘对齐，并置于父窗口最左边，会覆盖最左边的控件   
###android:layout_alignLeft   
	将该控件的左边缘与给定ID控件的左边缘对齐，并置于父窗口最上边，会覆盖最上边的控件   
###android:layout_alignRight   
	将该控件的右边缘与给定ID控件的右边缘对齐，并置于父窗口最上边，会覆盖最上边的控件   
###android:layout_alignTop   
	将给定控件的顶部边缘与给定ID控件的顶部对齐，并置于父窗口最左边，会覆盖最左边的控件