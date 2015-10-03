---
layout :  post
title : 源码阅读-apache common lang 3
---

### StringUtils——public构造函数
<p>{@code StringUtils} instances should NOT be constructed in
standard programming. Instead, the class should be used as
{@code StringUtils.trim(" foo ");}.</p>

<p>This constructor is public to permit tools that require a JavaBean
instance to operate.</p>
<pre class="prettyprint lang-java">
public StringUtils() {
    super();
}
</pre>
1、 一开始很奇怪，为什么Utils class会把构造函数设置为public，按理说应该设置为private，同时在构造函数中抛出异常，避免实际情况中生成对应的实例。
2、 注释很清楚的写着，某些场合需要一个JavaBean实例，如果那样的话就限制了这个class在那种场合的使用。
3、 **强加private构造函数限制看来是没有必要的，只是限制了class的使用场景，画蛇添足而已**。


### StringUtils——isEmpty的参数CharSequence
<pre class="prettyprint lang-java">
public static boolean isEmpty(final CharSequence cs) {
    return cs == null || cs.length() == 0;
}
</pre>
1、函数的参数是CharSequence而不是String，这里对什么是字符串做了一个更抽象的定义，字符串不仅仅是String类的实例，StringBuilder。。。类的实例也是字符串（任意的字符序列）。


### StringUtils——isBlank建议
<pre class="prettyprint lang-java">
public static boolean isBlank(final CharSequence cs) {
    int strLen;
    if (cs == null || (strLen = cs.length()) == 0) {
        return true;
    }
    for (int i = 0; i < strLen; i++) {
        //if (Character.isWhitespace(cs.charAt(i)) == false) {
        if (!Character.isWhitespace(cs.charAt(i))) {//这样子写，是不是可读性会更好一些。
            return false;
        }
    }
    return true;
}
</pre>

### StringUtils——trim参数为String
<pre class="prettyprint lang-java">
public static String trim(final String str) {
    return str == null ? null : str.trim();
}
</pre>
1、这里参数又变回来了，可能是考虑到只有String类有trim函数吧！


### StringUtils——trip中str判空多余
<pre class="prettyprint lang-java">
public static String strip(String str, final String stripChars) {
    if (isEmpty(str)) {//多余，下面两个函数都会进行等价的判断，考虑移除。
        return str;
    }
    str = stripStart(str, stripChars);
    return stripEnd(str, stripChars);
}
</pre>

### StringUtils——tripStart中建议用++start取代start++
<pre class="prettyprint lang-java">
public static String stripStart(final String str, final String stripChars) {
    int strLen;
    if (str == null || (strLen = str.length()) == 0) {
        return str;
    }
    int start = 0;
    if (stripChars == null) {
        while (start != strLen && Character.isWhitespace(str.charAt(start))) {
            start++;//建议用++start，考虑到效率
        }
    } else if (stripChars.isEmpty()) {
        return str;
    } else {
        while (start != strLen && stripChars.indexOf(str.charAt(start)) != INDEX_NOT_FOUND) {
            start++;//建议用++start，考虑到效率
        }
    }
    return str.substring(start);
}
</pre>

### StringUtils——stripAll建议使用已有的便利函数
<pre class="prettyprint lang-java">
public static String[] stripAll(final String[] strs, final String stripChars) {
       int strsLen;
       //建议使用ArrayUtils.isEmpty(strs);更清晰
       if (strs == null || (strsLen = strs.length) == 0) {
           return strs;
       }
       final String[] newArr = new String[strsLen];
       for (int i = 0; i < strsLen; i++) {
           newArr[i] = strip(strs[i], stripChars);
       }
       return newArr;
   }
</pre>

### StringUtils——indexOf参数是int
<pre class="prettyprint lang-java">
public static int indexOf(final CharSequence seq, final int searchChar) {
    if (isEmpty(seq)) {
        return INDEX_NOT_FOUND;
    }
    return CharSequenceUtils.indexOf(seq, searchChar, 0);
}
</pre>
1、这个地方有什么用意呢？
