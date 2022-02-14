
## Understanding the CSS z-index property.

**z-index property defines the stacking order** for HTML elements on a page.

![Photo by [Dan Burton](https://unsplash.com/@single_lens_reflex?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/9552/0*5uUMIMZMllXr1fJq)

Have you ever set a z-index value of 999999 for your element but still couldn’t manage to overlap that one other element. Let’s try to dig into this issue by getting a deeper understanding of the z-index.

### Why do we need z-index?

You must have heard about the 3 axes (x,y,z) in the cartesian plate. Most of the time we try to reposition our HTML elements on the x and y axes of the page with CSS but sometimes when they start overlapping each other we need to set the order of elements on the z-axis. That’s when the z-index comes into play.

 <iframe src="https://medium.com/media/0072db40921285c66dcb19d36a2ba00b" frameborder=0></iframe>

In the code above we have made 2 boxes and gave some -ve margins so that they can overlap with each other. We can see box1 is below box2. 
This was expected and this is because they are following the **Natural Stacking Order.**

### Natural Stacking Order

The natural stacking order is a set of rules our elements follow to order themselves on the page vertically. Below are the levels sorted in ascending order for priority.

* Background and borders of the element(lowest priority)

* Elements with negative stacking contexts, in order of appearance

* Non-positioned, floated elements, in order of appearance

* Inline elements, in order of appearance

* Positioned elements, in order of appearance(highest priority)

So, as per these rules, in the above codepen example, if you give *position: relative*(or any other position property except static) to box1 then it will come at the top of box2.

Now, since you have an idea about how elements are stacked together we can start on how z-index can help us tweak this natural stack according to our needs.

### **How does the z-index work?**
>  The **z-index** CSS property sets the z-order of a [positioned](https://developer.mozilla.org/en-US/docs/Web/CSS/position) element and its descendants or flex items. Overlapping elements with a larger z-index cover those with a smaller one.
>  - mdn docs

So, according to this, the element with the largest z-index value will be at the top of the page. When I first read this I thought this was the simplest concept in CSS. However, if you remember the bug we discussed in the starting, this concept is not solving it.
>  Why does a z-index value of 9999 can’t beat a lower z-index value sometimes?

The answer is **Stacking Context**.

 <iframe src="https://medium.com/media/c0c38ddcc0c6e616c12a4f2ba1252e07" frameborder=0></iframe>

### Stacking Context

 <iframe src="https://medium.com/media/b954e146d0ceee7c3c5669110618a82b" frameborder=0></iframe>

This pen is just the opposite of the first one in terms of the order of the boxes. Let’s check the CSS.

    .box{
      height:100px;
      width:100px;
      text-align:center;
    }

    .box1{
      background:red;
      position:relative;
      z-index:2;
    }

    .secondBoxWrapper{
      position:relative;
      z-index:1;
    }

    .box2{
      background:yellow;
      position:relative;
      z-index:999999;
      margin: -50px 0 -50px 50px;
    }

We have given here a z-index value of 2 to box1 and 999999 to box2. But still, box1 is overlapping box2. This is a simplified version of the bug we discussed in the beginning.

By now, you might have noticed that the secondBoxWrapper class having *z-index:1 *might be the culprit behind all this and you are absolutely right.
Here, secondBoxWrapper is creating a **Stacking Context **in which there is only 1 element i.e. box2.

But, **how did secondBoxWrapper created a new stacking context?**
It is because this time in the secondBoxWrapper class we have set position as relative and z-index as 1.

**Is there any other way to create these stacking contexts?
**Yes, there are multiple ways to create stacking contexts. A few of them are:

* Setting opacity to a value less than 1.

* Setting position to relative/absolute and give the z-index some value.
(this is the one we used).

* Setting position to fixed or sticky (No z-index needed for these values!).

* Adding a z-index to a child inside a display: flex or display: grid container.

* Using transform, filter, perspective etc.

You can find [the full list on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#the_stacking_context)

When a new stacking context is created with new stacking levels then they are independent of all other stacking contexts and stacking levels on the page.
All the children inside a stacking context are locked inside and they can’t compete with elements out of their context no matter how large their z-index value is.

For example here despite box2 having such a large z-index value it can’t compete with box1. The only one who can compete with box1 is secondBoxWrapper just because it has created a new stacking context. 
Try making another box(say box3) inside secondBoxWrapper and give some z-index to it with position relative. Now, box2 can compete with this box3.

### **How can we fix the above example?**

We want box2 with z-index: 999999 to beat box1 with z-index:2.

This can be done by removing the z-index property from the secondBoxWrapper class. This way secondBoxWrapper can’t create a new stacking context. Now, box1 and box2 will be in the same stacking context and when they compete, box2 will be the clear winner.

We can think of some other ways too but I am leaving this up to you. Try your thoughts in the examples above.

### Important points to keep in mind

 1. z-index won’t work without position property. Try setting z-index in the first pen without position property.
However, flex children can use z-index even if they’re statically-positioned.

 2. z-index values are auto/integer/inherit which are self-explanatory.

 3. z-index: auto does not create a stacking context. This is important because a parent with ‘auto’ will appear in front of a child with -1, but a parent with 0 will appear behind a child with -1.

### **Conclusion**

After all this, you might want to say this to z-index.

![](https://cdn-images-1.medium.com/max/2000/1*wTJcZDYkp9K6qeiqJGnhew.png)

But, if there were no stacking contexts we would have to give different z-index values every time we wanted to tweak the natural order. For big projects that would be a really tiresome task.
For most of the problems, making sure that you don’t have parent elements limiting the z-index level of their children can do the trick.