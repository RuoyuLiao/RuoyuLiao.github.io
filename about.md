---
layout: page
title: "About"
description: "Hungry & Foolish."
header-img: "img/post-bg-rwd.jpg"
---

<!-- Language Selector -->
<select class="sel-lang" onchange= "onLanChange(this.options[this.options.selectedIndex].value)">
    <option value="0" selected> 中文 Chinese </option>
    <option value="1"> 英文 English </option>
</select>

<!-- Chinese Version -->
<div class="zh post-container">
    <blockquote><p>多容寡欲，千里江河</p></blockquote>

    <p>程序猿，在北京。</p>

    <p>这是利用 <a href="https://pages.github.com/">GitHub Pages</a> 与 <a href="http://jekyll.com.cn/">Jekyll</a> 搭建的 个人博客。我在GitHub主页<a href="https://github.com/longwind09">👉GitHub·longwind09</a> 与 简书主页<a href="https://http://www.jianshu.com/u/ec260083e70e">👉longwind09</a>。</p>

    <h5>经历</h5>

    <ul>
    <li>2016.7-今，58赶集算法工程师</li>
    <li>2015.9-2016.7，58同城搜索实习</li>
    <li>2013.9-2016.7, 北京化工大学计算机科学与技术研究生(智能工程研究室)</li>
    <li>2009.9-2013.7, 北京化工大学计算机科学与技术本科</li>
    </ul>

    
</div>

<!-- English Version -->
<div class="en post-container">
    <blockquote><p>Yet another Programmer. <br> </p></blockquote>

    <strong>Felix</strong>. major in data science and software

    This blog is made with Github Pages and Jekyll. My GitHubGithub·[longwind09](http://github.com/longwind09)
    
    <h5>Resume</h5>

    <ul>
    <li>2016.7-今，58赶集算法工程师</li>
    <li>2015.9-2016.7，58同城搜索实习</li>
    <li>2013.7-2016.7, 北京化工大学计算机科学与技术研究生(智能工程研究室)</li>
    <li>2009.9-2013.7, 北京化工大学计算机科学与技术本科</li>
    </ul>

</div>

<!-- Handle Language Change -->
<script type="text/javascript">
    // get nodes
    var $zh = document.querySelector(".zh");
    var $en = document.querySelector(".en");
    var $select = document.querySelector("select");

    // bind hashchange event
    window.addEventListener('hashchange', _render);

    // handle render
    function _render(){
        var _hash = window.location.hash;
        // en
        if(_hash == "#en"){
            $select.selectedIndex = 1;
            $en.style.display = "block";
            $zh.style.display = "none";
        // zh by default
        }else{
            // not trigger onChange, otherwise cause a loop call.
            $select.selectedIndex = 0;
            $zh.style.display = "block";
            $en.style.display = "none";
        }
    }

    // handle select change
    function onLanChange(index){
        if(index == 0){
            window.location.hash = "#zh"
        }else{
            window.location.hash = "#en"
        }
    }

    // init
    _render();
</script>




