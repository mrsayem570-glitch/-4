<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ad System</title>

<style>
body{
    background:#111;
    color:#fff;
    text-align:center;
    font-family:Arial;
}

button{
    padding:12px 25px;
    border:none;
    border-radius:6px;
    background:#00ffcc;
    font-size:16px;
}

#circle{
    width:120px;
    height:120px;
    border-radius:50%;
    margin:20px auto;
}
</style>
</head>

<body>

<h2>Earn Points</h2>

<p>Ads: <span id="ads">0</span></p>
<p>Points: <span id="points">0</span></p>

<div id="circle"></div>
<p id="percent">0%</p>

<button id="btn">Loading...</button>

<!-- Monetag Script -->
<script src="https://libtl.com/sdk.js"
data-zone="10852660"
data-sdk="show_10852660"></script>

<script>

let ads = 0;
let points = 0;
let btn = document.getElementById("btn");

function update(){
    document.getElementById("ads").innerText = ads;
    document.getElementById("points").innerText = points.toFixed(2);

    let p = Math.min((ads/10)*100,100);
    document.getElementById("percent").innerText = p+"%";

    document.getElementById("circle").style.background =
    `conic-gradient(#00ffcc ${p}%, #222 ${p}%)`;
}

// SDK CHECK
function ready(){
    if(typeof window.show_10852660 === "function"){
        btn.innerText = "Watch Ad";
        btn.disabled = false;
    }else{
        btn.innerText = "Demo Ad";
        btn.disabled = false;
    }
}

setTimeout(ready,3000);

// CLICK
btn.onclick = function(){

    if(typeof window.show_10852660 === "function"){
        show_10852660().then(()=>{
            ads++;
            points += 0.5;
            update();
        }).catch(()=>{
            alert("Ad failed");
        });
    }else{
        alert("Demo Ad Played ✅");
        ads++;
        points += 0.5;
        update();
    }
}

update();

</script>

</body>
</html>
