---
layout: post
title: "Why is Git so bad at files?"
date: 2014/10/13
categories: git
---

    git filter-branch --tree-filter 'if [ -f obffb.js ]; then mv obffb.js javascript1.js; fi' HEAD && git push origin master --force

I had to do *all of that*, just to **rename a file!**

Okay, so for those of you who aren't familiar with Git: It's a content tracker that keeps track of stuff (usually code) for you. Namely, the key stuff thing that I'm talking about here is revision history. Git is nice because it stores the history of all of your files, and I'm currently obfuscating some code (here's the final product:

    http://keyboardfire.com/ | license: MIT | contact/email: andy@<website> | enjoy!
    (U=function(o){this.Q=o}).prototype.w=function(M){J='ns',H=Math.PI,G='.',T=H|0+G
    E=function(b){return b.replace(Q[T],function(b){return h(b.charCodeAt()-H+T)})};
    return-M,(l=this.Q)+Array(T).join((h=l.constructor.fromCharCode)(0x79+U.length))
    };function F(){}g=((B=function(){return[].slice.call(arguments).join('o')}),F)//
    function C(r,p,C){return eval(x="while(p=((p\x7c\1744)-1))C=(C?(C+r)\x3a''+r)")}
    Y=C(),(b=new U(g.name+C(x[x=2],-(~-[]*x)))).w();Y=Y.slice(4,7);F.L=25*+([]+H)[T]
    f=new U(371..toString(31,Y).replace(/./,function(x){return x.toUpperCase()}));{}
    for(i=s=0;i++<F.L;s=Array(+'')+[]){Q=['le','hm',['%',T+74],new RegExp(G,'g',J)];
    if(!(i%Y.length))s+=b[unescape(Q[2].join(''))]();i%x.indexOf('(')||Y[[]]||(s+=f.
    w());eval(B('c',J,Q[0]))[E(Q[1]).split('').reverse().join(h(C(1)))](s||U.g||i);}

). The revision history is quite useful in this case because you can see how the code evolved and changed. However! Problem happened.

Originally, the file was called `obffb.js`. I wanted to rename it to `javascript1.js` in my git repo. So I did that, which completely destroyed the revision history. See, git keeps track of renames by simply deleting the old file, and creating a new file with the same content (which is actually exactly what's happening, but not what most people think / want). So the entire history of the file went boom. Okay, let's reset that.

    llama@llama:~/Code/web/obffizzbuzz3$ git reset --hard HEAD~1 && git push -f

Now after a bit of Googling, I found `git filter-branch --tree-filter`, which can rewrite a tree and all of its contents. So I had this:

    llama@llama:~/Code/web/obffizzbuzz3$ git filter-branch --tree-filter ':' HEAD

Now what? Well, I just want to rename a file:

    llama@llama:~/Code/web/obffizzbuzz3$ git filter-branch --tree-filter 'mv obffb.js javascript1.js' HEAD

But that would bork in the early revisions when there *was* no `obffb.js`. So after a bit more Google I figured out I could use a `-f` thingy, and I wrote an if statement:

    llama@llama:~/Code/web/obffizzbuzz3$ git filter-branch --tree-filter 'if [ -f obffb.js ]; then mv obffb.js javascript1.js; fi' HEAD

And then pushed it back out:

    llama@llama:~/Code/web/obffizzbuzz3$ git push origin master

After a quick check with `git status` it says that I'm apparently missing some changes even though I *just pushed*, so I used the force, Luke:

    llama@llama:~/Code/web/obffizzbuzz3$ git push origin master --force

And it worked! **Finally**.

Why is Git so bad at files?
