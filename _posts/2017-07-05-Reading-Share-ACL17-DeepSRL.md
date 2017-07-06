---
layout: plain
title: RL Chapter14 Psychology Report
dec: Share Reading Reading "ACL17 DeepSRL"
excerpt: 一个新的SRL模型，4层双向LSTM + highway + RNN dropout
category: tech
---


### Model

1. applying recent advances in training deep recurrent neural networks such as highway connections (Srivastava et al., 2015) 
2. RNN-dropouts (Gal and Ghahramani, 2016).
3. using an A\* decoding algorithm (Lewis and Steedman, 2014; Lee et al., 2016) to enforce structural consistency at prediction time without adding more complexity to the training process.


### Analysis is complete

- What is the model good at and what kinds of mistakes does it make?
- How well do LSTMs model global structural consistency, despite conditionally indepen- dent tagging decisions?
- Is our model implicitly learning syntax, and could explicitly modeling syntax still help?


<a class="media" href="/assets/file/Share-ACL17-DeepSRL-What-works-what's-next.pdf">
<div style="font-size: 0">
  <script type="text/javascript" style="font-size: 0">
  document.ready = function() {  
        $('a.media').media({width:"100%", height:600});  
  };
 </script>
</div>
