---
title:  "순열과 조합"
categories: 
  - c++
---
<div style="font-family: 'Lucida Grande', 'Segoe UI', 'Apple SD Gothic Neo', 'Malgun Gothic', 'Lucida Sans Unicode', Helvetica, Arial, sans-serif; font-size: 0.9em; overflow-x: hidden; overflow-y: auto; margin: 0px !important; padding: 5px 20px 26px !important; background-color: rgb(255, 255, 255);font-family: 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; padding: 20px;padding: 20px; color: rgb(34, 34, 34); font-size: 15px; font-family: 'Roboto Condensed', Tauri, 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; line-height: 1.6; -webkit-font-smoothing: antialiased; background: rgb(255, 255, 255);"><h3 id="조합과-순열" style="clear: both;font-size: 1.6em; font-weight: bold; margin: 1.125em 0px 0.75em;margin-top: 0px;"><a name="조합과-순열" href="#조합과-순열" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>조합과 순열</h3><h5 id="조합" style="clear: both;font-size: 1.2em; font-weight: bold; margin: 0.855em 0px 0.57em;"><a name="조합" href="#조합" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>조합</h5><p style="margin-top: 0px;margin: 1em 0px; word-wrap: break-word;">순서를 고려하여 n개 중에서 r개를 뽑는 것<br style="clear: both;">(1,2) 와 (2,1)을 다른 경우로 본다</p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>int T[10]; //nPr을 이루는 각각의 경우를 저장
int data[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};

void swap(int *a, int *b){
    int t;
    t = *a;
    *a = *b;
    *b = t;
}

void perm(int n, int r){
    if(r==0){
        for(int i=0;i&amp;lt;length;i++){
            printf(&quot;%d &quot;,T[i]);
        }
        printf(&quot;\n&quot;);
        return;
    }else if (n&amp;lt;r){
        return;
    }
    for(int i= n-1 ; i&amp;gt;=0 ;i--){

        // 1234 , 4231 , 1432 , 1243 -&amp;gt; 이런식으로 맨 뒤에 여러개의 숫자가 들어갈 수 있도록
        swap(&amp;amp;data[i], &amp;amp;data[n-1]); //n-1을 모든 index와 swap해서 다양한 순서를 만든다.
        T[r-1] = data[n-1];          //T의 뒤에서부터 결과값 저장
        perm(n-1, r-1);          //다음  index로 진행

        //원상 복구
        swap(&amp;amp;data[i], &amp;amp;data[n-1]);
    }

}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> T[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>]; <span class="hljs-comment" style="color: rgb(147, 161, 161);">//nPr을 이루는 각각의 경우를 저장</span>
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> data[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>] = {<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">4</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">5</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">6</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">7</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">8</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">9</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>};

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">swap</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> *a, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> *b)</span></span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> t;
    t = *a;
    *a = *b;
    *b = t;
}

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">perm</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> n, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> r)</span></span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(r==<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>){
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;length;i++){
            <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d "</span>,T[i]);
        }
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"\n"</span>);
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
    }<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">if</span> <span class="hljs-params">(n&lt;r)</span></span>{
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
    }
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i= n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span> ; i&gt;=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span> ;i--){

        <span class="hljs-comment" style="color: rgb(147, 161, 161);">// 1234 , 4231 , 1432 , 1243 -&gt; 이런식으로 맨 뒤에 여러개의 숫자가 들어갈 수 있도록</span>
        swap(&amp;data[i], &amp;data[n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>]); <span class="hljs-comment" style="color: rgb(147, 161, 161);">//n-1을 모든 index와 swap해서 다양한 순서를 만든다.</span>
        T[r-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>] = data[n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>];          <span class="hljs-comment" style="color: rgb(147, 161, 161);">//T의 뒤에서부터 결과값 저장</span>
        perm(n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>, r-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);          <span class="hljs-comment" style="color: rgb(147, 161, 161);">//다음  index로 진행</span>

        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//원상 복구</span>
        swap(&amp;data[i], &amp;data[n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>]);
    }

}
</code></pre><h5 id="순열" style="clear: both;font-size: 1.2em; font-weight: bold; margin: 0.855em 0px 0.57em;"><a name="순열" href="#순열" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>순열</h5><p style="margin-top: 0px;margin: 1em 0px; word-wrap: break-word;">순서에 상관없이 n개중 r개를 뽑는 경우</p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>
int T[10]; //nPr을 이루는 각각의 경우를 저장
int data[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 0};
int length = 4;

void comb(int n, int r){
    if(r == 0){
        for(int i=0;i&amp;lt;length;i++){
            printf(&quot;%d &quot;,T[i]);
        }
        printf(&quot;\n&quot;);
        return;
    }else if(n&amp;lt;r){
        return;
    }
    else {
        T[r-1] = data[n-1];
        comb(n-1, r-1);  //n-1Cr-1: 현재 아이템을 선택한 경우
        comb(n-1, r);    //n-1Cr: 현재 아이템을 선택하지 않은 경우
    }
}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;">
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> T[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>]; <span class="hljs-comment" style="color: rgb(147, 161, 161);">//nPr을 이루는 각각의 경우를 저장</span>
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> data[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>] = {<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">4</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">5</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">6</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">7</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">8</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">9</span>, <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>};
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> length = <span class="hljs-number" style="color: rgb(42, 161, 152);">4</span>;

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">comb</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> n, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> r)</span></span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(r == <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>){
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;length;i++){
            <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d "</span>,T[i]);
        }
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"\n"</span>);
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
    }<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">if</span><span class="hljs-params">(n&lt;r)</span></span>{
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
    }
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span> {
        T[r-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>] = data[n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>];
        comb(n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>, r-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);  <span class="hljs-comment" style="color: rgb(147, 161, 161);">//n-1Cr-1: 현재 아이템을 선택한 경우</span>
        comb(n-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>, r);    <span class="hljs-comment" style="color: rgb(147, 161, 161);">//n-1Cr: 현재 아이템을 선택하지 않은 경우</span>
    }
}
</code></pre></div>
