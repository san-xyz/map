// Scoreboard.js by ŚĄŃ
 var script=document.createElement('script');
script.src="https://www.gstatic.com/firebasejs/4.13.0/firebase.js";
document.head.appendChild(script);
var Scoreboard=function(config){
var style=document.createElement('style');
var link=document.createElement('link');
var div=document.createElement('div');
div.style.position='fixed';
link.href="https://fonts.googleapis.com/css2?family=Varela+Round&display=swap"
link.rel='stylesheet'
style.innerHTML="#CON{height:100vh;width:100vw;background:rgba(0,0,0,.2);position:fixed;left:0;top:0;font-family: 'Varela Round', sans-serif;display:none;}#SBD { display:block;position:relative;top:8vh;margin:auto;height:75vh;width:78vw;padding:20px 3px 3px 3px;background:white;border-radius:4.5vw;box-shadow:0 0 2px gray;}#US{position:absolute; width:78vw;height:75vh;background:rgb(220,220,220);border-radius:4vw; }#LAB{width:100%;position:absolute;left:0;top:0;  text-align:center;font-size:10px;color:gray;padding:4px;}#STPF{height:73vh;  width:76vw;position:absolute;top:1vw;left:1vw; overflow-y:scroll;  overflow-x:hidden;border-radius:5px;}.STP{position:relative;width:76vw;margin-bottom:1vw;height:14vw;   background:white;border-radius:3vw;}.RANK{height:3.5vw;width:20vw;  background:rgba(210,0,300,.3);font-size:3vw;border-radius:1000px;text-align:center;font-weight:1000;position:absolute;right:28vw;top:1vw;}.TIME{height:6.5vw;width:35.5vw;  background:rgba(210,0,300,.1);font-size:2.7vw;border-radius:2vw;font-weight:1000;position:absolute;right:1vw;bottom:1vw;padding:.4vw 0 0 1.2vw;}.NAME{height:6.5vw;width:35.5vw;background:rgba(210,0,300,.1);font-size:2.7vw;border-radius:2vw;font-weight:1000;position:absolute;left:1vw;bottom:1vw;padding:.4vw 0 0 1.2vw;}#CANCEL{width:25vw;padding:3px 6px 1px 6px;  background:white;text-align:center;position:absolute;top:90vh;left:37.5vw;border-radius:20vh;}";

div.innerHTML="<div id='CON'><div id='SBD'><div id='LAB'>ŚĄŃ SCOREBOARD</div><div id='US'><div id='STPF'></div></div></div> <div id='CANCEL'>CANCEL</div></div>"
document.head.appendChild(style);
document.head.appendChild(link);
document.body.appendChild(div);
firebase.initializeApp(config); 

Scoreboard.show=function(order){
document.getElementById('CON').style.display='block';  
firebase.database().ref("scores").orderByChild(order).limitToLast(100).on("value", 
function(snapshot){
var scoresList = [];
snapshot.forEach(function(child) {
scoresList.push({
name:child.val().name,score: child.val().score,time: child.val().time});});
scoresList.reverse();
document.getElementById('STPF').innerHTML='';
for(var i=0;i<scoresList.length;i++){var rank=i+1;
document.getElementById('STPF').innerHTML+=User(rank,scoresList[i].name,scoresList[i].score,scoresList[i].time);
document.getElementById('n'+rank).textContent=scoresList[i].name;
}
});
};
var User=function(rank,name,score,date){
var x=rank==1?"style='background:gold;'":'';
var y=rank==1?"style='background:rgba(255,215,0,.3);'":'';
var t=date.split(' ');
return "<div class='STP'><div class='RANK'"+x+">TOP #"+rank+"</div><div class='TIME'"+y+"> TIME : "+t[4]+"<br> DATE : "+t[2]+" "+t[1]+" "+t[3]+"</div><div class='NAME'"+y+"><div style='width:100vw;'> NAME : <span id='n"+rank+"'></span><br> SCORE : "+score+"</div></div></div>";
}
var LIMIT=function(s,l){var o=s.split(''),NODE="";
for(var i=0;i<l;i++){NODE+=o[i]};
return s.length<l?s:NODE;
}
Scoreboard.pushScore=function(n,s){
var sc=typeof s !="number"?0:s;
typeof s !="number"?console.log("ERROR : Score should be a number."):'';
if(typeof s == "number"){
firebase.database().ref("scores").push({
name:LIMIT(n,15),score:sc<=9999999999?sc:9999999999,time:new Date().toString()});}
}
Scoreboard.clearRecords=function(){
firebase.database().ref("scores").remove()
}
document.getElementById('CANCEL').onclick=function(){document.getElementById('CON').style.display='none'}
};
