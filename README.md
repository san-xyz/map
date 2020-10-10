# map
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
    </head>
    <body>
<canvas></canvas>   
<script>
window.onload = function () {
var c = document.querySelector("canvas");
var san = c.getContext("2d");
var ar = [
[1,1,1,1,1,1,0,1,1,1,1,1,1,0,1,1,0,0,0,1],
[1,0,0,0,0,0,0,1,0,0,0,0,1,0,1,0,1,0,0,1],
[1,0,0,0,0,0,0,1,0,0,0,0,1,0,1,0,1,0,0,1],
[1,1,1,1,1,1,0,1,1,1,1,1,1,0,1,0,0,1,0,1],
[0,0,0,0,0,1,0,1,0,0,0,0,1,0,1,0,0,1,0,1],
[0,0,0,0,0,1,0,1,0,0,0,0,1,0,1,0,0,1,0,1],
[1,1,1,1,1,1,0,1,0,0,0,0,1,0,1,0,0,0,1,1]
   ];
for(var o=0;o<ar.length;o++) {
for(var i=0;i<ar[o].length;i++) {
if(ar[o][i] === 1) {
size = 5;
ar[o][i] = san.rect(i*size,o*size,size,size);};
}
}
ar;
san.fillStyle="blue";
san.fill();
}
</script>     
    </body>
</html>
