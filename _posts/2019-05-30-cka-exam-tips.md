---
layout: post
title:  " cka exam tips "

categories: jekyll update
---

[https://linuxacademy.com/community/posts/show/topic/25094-cka-exam-experience-and-some-useful-tips](https://linuxacademy.com/community/posts/show/topic/25094-cka-exam-experience-and-some-useful-tips)



```
Hello All,

As promised I am making a short post to describe my experience with the CKA exam and share a few tips that I think would be helpful.

Please note that my grade was not that impressive (81% although i had not touched 12% due to lack of time ... more on that later), and everyone has his/her own way and style, but I am trying to share things which I believe helped me pass despite my mistakes, after all, we learn from mistakes the most  and I am not ashamed of sharing them :)

So let me begin with my mistakes which I advise everyone to avoid:

    I depended on Kubeadm installations....DO NOT.....i repeat...DO NOT practive on kubeadm installations only... Go to this https://github.com/kelseyhightower/kubernetes-the-hard-way and just keep repeating it as often as you can, my mistake was that I did it twice only and the first was by blind copy and paste without much thinking.
    I Did not practice topics beyond this course and depended on the practice exam only.... make sure you do go to the official kubernetes documentation and search every other object type and option not covered in this course and try to practice it as well. I got hit with 3 or 4 surprises, API objects/options which I never knew even existed in  Kubernetes to be honest, it was straightforward to understand and use but it meant a lot of extra time was spent on them which caused me to not be able to finish 2 questions towards the end (one for 4% and another for 8%).
    Tried to copy and paste from the exam terminal, I probably wasted 5 mins (yes even 5 mins matter out of the 3 hours) trying to copy and paste from that terminal..... never do that.... trust me it is better to type things.
    Got lenient a bit with my time in the middle of the exam thinking that I have good progress and time will be more than enough which made me get too much of a "perfectionist" and always triple checking (not just double) my answers....DO NOT do that....every minute counts trust me on that and the questions begin to get harder and more complicated towards the end.
    I had basic understanding of Certificates and Keys....that was a huge mistake when attempting this exam....but it is a well learnt lesson and now I will be delving deeper into understanding that topic properly.

Sorry for the lengthy post but I still have my personal tips to share which are:

    Do not be ashamed or reluctant to use the docs and copy anything even yaml files. According  to the proctor for my exam you have UNLIMITED internet access....you can literally google anything (well except CKA exam material of course so don't try to login to linux academy and watch a video or something :) ).
    When you search on docs for something use e.g: "deployment yaml" and you will find a page with a yaml file that you can wget and then edit it as the question asks before creating it.
    Use VIM editor ....Use VIM editor.......USE VIM EDITOR... sorry for yelling that and  sorry Chad I know you like Nano :D  but it is essential for lots of time saving ... simple tricks like ":%s/foo/bar/" which would replace all entries of "foo" in the file with "bar" would allow you to easily and quickly reuse yaml files without wasting time, I probably did that 5 or 6 times during the exam... also when you copy a yaml and it has a huge chunk you want to get rid of "dG" deletes from the line your cursor is at till the end of the file ... trust me ...every tap on your keyboard will matter... 
    Use the built-in notepad in the exam controls, will be very handy to manipulate text before using it in the terminal.
    Use tmux when you want to need to SSH to more than one machine at once in the cluster and if you find yourself having to do repetitive commands which are common between all then just use the ":setw synchronize-panes" option which is pretty self-explanatory, every command you type in one pane is typed in the others and runs there as well ...  here is a tmux cheatsheet and the learning curve is .... ummm .......5 mins ? lol (for what you might need for the exam I mean such as spliting the screen to a few panes and such) .... https://gist.github.com/MohamedAlaa/2961058
    If you do not know how Systemd works, DO NOT attempt the exam untile you are familiar with that (I am not an expert but I know what my LFCS cert taught me which I learnt here at LA as well), point is....you need at least an intermediatry level of linux experience.... some awk and cut tricks might come in handy as well.

Again, I apologise for the lengthy post but I hope this can benefit as many fellow students as possible so that they can go out there and ace the exam because if you take the great course here at LA, add to it your own hardwork and continuous practice and familiarize yourself with as much of the documentation as possible, you will pass with ease.... Good luck everyone and best regards!!! 
```

