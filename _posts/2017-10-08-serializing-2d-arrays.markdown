---
layout: post
title:  "Getting Unity To Serialize 2D Arrays"
---
You’ve got a 2D array that you’d like to serialize, persist, or even just show up in the inspector. You’ve tried making the 2D array public, or slapping `[SerializeField]` on the declaration, but to no avail, Unity just seems to ignore it.

It turns out that Unity doesn’t support serializing multidimensional arrays. However, with a little extra effort, you can convince Unity to serialize them just fine.

A simple approach is to ‘wrap’ a class around an array, and then make an array of this wrapper class. Sounds a bit confusing, but the example code below should help clear things up a bit.

By using this approach, Unity will serialize and persist your 2D array just like you’d expect. It also allows you to view and edit your 2D array in the inspector, without needing to write your own custom property drawer.

Let’s use a 2D array of ints as an example, we’ll call it an ‘IntGrid’.

{% highlight csharp %}
[System.Serializable]
public class IntGrid {

	[System.Serializable]
	public class IntRow {
		public int[] Cols; // The wrapped array.
	}

	public IntRow[] Rows; // The 2D array.
}
{% endhighlight %}

That’s all you need to get Unity to serialize your 2D array and have it show up in the inspector.

Let’s overload the `[,]` operator so we can get and set data the way we’re used to.

{% highlight csharp %}
[System.Serializable]
public class IntGrid {

	...

	public int this[int rowIndex, int colIndex] {
		get { return Rows[rowIndex].Cols[colIndex]; }
		set { Rows[rowIndex].Cols[colIndex] = value; }
	}
}
{% endhighlight %}

Now we can treat an instance of our ‘IntGrid’ as if it were a regular 2D array.

{% highlight csharp %}
myGrid[0, 0] = 64;
int value = myGrid[0, 0];
{% endhighlight %}
