<!DOCTYPE html>
<head>
<script src="/assets/jquery.js"></script>
<link href='https://fonts.googleapis.com/css?family=Londrina+Shadow' rel='stylesheet' type='text/css'>
<style>
body {
  font-family: helvetica, sans-serif;
  margin: 0 auto;
  max-width: 600px;
  background: #232323;
}
div {
  height: 300px;
  background-size: cover;
  position: relative;
  margin: 40px 0 0 0;
  border-radius: 12px;
}
h1 {
  font-family: 'Londrina Shadow', cursive;
  text-align: center;
  font-size: 75px;
  color: #aaaaaa;
  margin: 60px 0 0 0;
}
h2 {
  text-align: center;
  color: #bbbbbb;
  margin: 0px 0 70px 0;
}
p {
  color: rgba(255,255,255,1);
  background: black;
  background: linear-gradient(bottom, rgba(0,0,0,1), rgba(0,0,0,.4));
  background: -webkit-linear-gradient(bottom, rgba(0,0,0,1), rgba(0,0,0,.4));
  background: -moz-linear-gradient(bottom, rgba(0,0,0,1), rgba(0,0,0,.4));
  padding: 10px;
  line-height: 28px;
  text-align: justify;
  position: absolute;
  bottom: 0;
  margin: 0;
  height: 30px;
  transition: height .5s;
  -webkit-transition: height .5s;
  -moz-transition: height .5s;
}

small {
  opacity: 0;
}

.show-description p {
  height: 150px;
}

.show-description small {
  opacity: 1;
}

.price {
  float: right;
}
@media (max-width: 500px) {
  h1 {
    font-size: 50px;
    margin-top: 20px;
    line-height: 40px;
  }
  h2 {
    font-size: 20px;
    margin: 20px 0 30px 0;
  }
  div {
    margin: 20px 12px 0 12px;
  }
  p {
    font-size: 20px;
    line-height: 24px;
  }
  small {
    font-size: 16px;
  }
}
li {
      display: inline;
      padding: 0px 10px 0px 10px;
}
 ul {
     text-align: center;
 }

</style>

</head>

<body>
    <ul>
      <li><button onclick=stocks()>stocks</button></li>
      <li><button onclick=shop()>shop</button></li>
      <li><button onclick=sell()>sell</button></li>
    </ul>
<h1>rodney's sneaker shop</h1>
<h2>a New York City sneak shop</h2>

<div id="rodney">
</div>

<script>
jordansImages = [
  'url("https://i1.wp.com/www.nicekicks.com/files/2015/05/where-to-buy-air-jordan-1-chicago-online-for-sale.jpg?fit=759%2C400&ssl=1")',
  'url("https://images.solecollector.com/complex/image/upload/lp5jbgtdnssvwvi2iaei.jpg")',
  'url("https://cdn5.kicksonfire.com/wp-content/uploads/2016/11/Air-Jordan-9-Space-Jam-2-565x372.jpg?x65229")',
  ]
stocksImages = [ 
  'url("https://proxy.markets.businessinsider.com/cst/MarketsInsiderV2/Share/chart.aspx?instruments=161,766143,161,538&style=instrument_realtime_data_year&period=OneYear&timezone=Eastern%20Standard%20Time")',
  'url("https://proxy.markets.businessinsider.com/cst/MarketsInsiderV2/Share/chart.aspx?instruments=899,957150,899,333&style=instrument_realtime_data_year_0digit&period=OneYear&timezone=Eastern%20Standard%20Time")',
  'url("https://proxy.markets.businessinsider.com/cst/MarketsInsiderV2/Share/chart.aspx?instruments=16,11730015,16,814&style=instrument_realtime_data_year_0digit&period=OneYear&timezone=Eastern%20Standard%20Time")',
  ]
sellImages = [ 
  'url("https://ssl.c.photoshelter.com/img-get/I00004JAf5nTEDe4/s/900/720/Sneaker-Con-706.jpg")',
  'url("data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBw0NDQ0NDQ0NDQ0NDQ0NDQ0NDQ8NDQ0NFREWFhURExUYHSggGBoxGxUVITEhJSkrLi4uFx8zODMtNygtOisBCgoKDg0NFQ8PFSsZFRkrKysrKy0rKy0tLTctLS0rLTc3LSsrKys3LS0tNzc3Nzc3KystNzcrLSstLS0tNy0rK//AABEIALcBEwMBIgACEQEDEQH/xAAXAAEBAQEAAAAAAAAAAAAAAAAAAQIH/8QAIRABAAICAgIDAQEAAAAAAAAAAAERkfAxYSGhAnGBURL/xAAWAQEBAQAAAAAAAAAAAAAAAAAAAQL/xAAXEQEBAQEAAAAAAAAAAAAAAAAAAREx/9oADAMBAAIRAxEAPwDiMSQzDUI0oCKlJMkyKjICsrfhAkCGmYaSrGUVFQAAABbQAAAAAAAAAAAAAAAAAWG4Yb+KVYoWzMo0tFESojCKktMo1DICqyAqC0CC0gAAAAAAAAAAAAApMAgAAoLiCgmDXxZa+JVhMgqNRFlFoRlAVkMAC39F9oYFW+y+5L+i+0FvuUvv0t9+i+/QMz9i4J/FECgQRVroEpFyt9gyNX3BgVka/ISRAEBUUFAEUAAa+LLXxWpEWEkQGmVF4yArIAAioClgCxP0uGVwimDB+QV1GQK6Ra6RQwv4gCmEXAGCuiuklAQFQAAW0AaooEaQUBGviysKytFJa2ilLJaWKyArIAAgoAALG2fhvkrpFK69ldeyuiugK69mSuvZkEAUUwWiB+IqKgAAAAACwrKwLGhLEXT/ACizKUqULKKELLKQFAAABFRQAAXfJXRvkRSuiuvZvJvIFdewwAG+BFFTCphARUVAAAAAAAAAAGiARQkAQKFQAkAAEUAAN6Bd8mAwimEwu8G8KJhcGcG8IAVsG+QDeDfBkERUVBUUAVJFqDSBiACAANLRCo0iLIAioIkqSioCoAEgAKBvgyb/AA3lFMm8m8pgF3kyYQFwZEAFRQQBAFBFhAFCJVGkRRUxBUEasSZLRSZIRYVFIURUlAVFEUEkJIABQEwu/wAMooZwG8gZTeFxk3kEFRQBBBUAURRRFEMRQUUBGgAGRaFYRYlAFmRABSgAACSCSAFRQEU3kEXeDeTeUU3g3g3k3kDCFioIACiAqKUKKgigqAAAogDTMyvK0DCxC/JIVlqUiAlFJlIapAQUUQgkgQBQQVBQAQsAAAEBQRYEBQEaAAAAAAABGk/0AVGrBTSwEEmSgBUACUBQUBBAFVABUAQEAUoAJQAFgBVQEUAVABFAFH//2Q==")',
  ]
  
stocksDivs = [ 
  '<div class="item"><p>CHICAGO OG 1s<span class="price">$</span><br /><small>Mustard sierra leone bologi. </small></p></div>',
  '<div class="item"><p>pastrami boudin tongue <span class="price">$22</span><br /><small>Tri-tip capicola kielbasa bresaola. </small></p></div>',
  '<div class="item"><p>fruitcake marzipan pudding dragee <span class="price">$8</span><br /><small>Lollipop ice cream candy canes.</small></p></div>',
  ]
  
shopDivs = [ 
  '<div class="item"><p>welsh onion soko <span class="price">$14</span><br /><small>Mustard sierra leone bologi. </small></p></div>',
  '<div class="item"><p>pastrami boudin tongue <span class="price">$22</span><br /><small>Tri-tip capicola kielbasa bresaola. </small></p></div>',
  '<div class="item"><p>fruitcake marzipan pudding dragee <span class="price">$8</span><br /><small>Lollipop ice cream candy canes.</small></p></div>',
  ]
  
  sellDivs = [ 
  '<div class="item"><p>welsh onion soko <span class="price">$14</span><br /><small>Mustard sierra leone bologi. </small></p></div>',
  '<div class="item"><p>pastrami boudin tongue <span class="price">$22</span><br /><small>Tri-tip capicola kielbasa bresaola. </small></p></div>',
  '<div class="item"><p>fruitcake marzipan pudding dragee <span class="price">$8</span><br /><small>Lollipop ice cream candy canes.</small></p></div>',
  ]
  
  $('div').on('click', function() {
      $(this).toggleClass('show-description');
  });
  

  
function stocks() {
    james= document.getElementById("rodney")
    james.innerHTML = ''
	   james.innerHTML += stocksDivs[0]
     james.innerHTML += stocksDivs[1]
     james.innerHTML += stocksDivs[2]

	//alert("you've clicked stocks")
	items = document.getElementsByClassName("item")
	items[0].style.background = stocksImages[0]
	items[0].style.backgroundSize = '100% 100%'
  items[1].style.background = stocksImages[1]
  items[1].style.backgroundSize = '100% 100%'
  items[2].style.background = stocksImages[2]
  items[2].style.backgroundSize = '100% 100%'
} 

function shop() {
  jack= document.getElementById("rodney")
     jack.innerHTML = ''
	   jack.innerHTML += shopDivs[0]
     jack.innerHTML += shopDivs[1]
     jack.innerHTML += shopDivs[2]
	//alert("you've clicked shop")
	items = document.getElementsByClassName("item")
	items[0].style.background = jordansImages[0]
	items[0].style.backgroundSize = '100% 100%'
  items[1].style.background = jordansImages[1]
  items[1].style.backgroundSize = '100% 100%'
  items[2].style.background = jordansImages[2]
  items[2].style.backgroundSize = '100% 100%'
} 

function sell() {
    mak= document.getElementById("rodney")
     mak.innerHTML = ''
	   mak.innerHTML += sellDivs[0]
     mak.innerHTML += sellDivs[1]
     mak.innerHTML += sellDivs[2]
	//alert("you've clicked sell")
	items = document.getElementsByClassName("item")
	items[0].style.background = sellImages[0]
	items[0].style.backgroundSize = '100% 100%'
	items[1].style.background = sellImages[1]
  items[1].style.backgroundSize = '100% 100%'
  items[2].style.background = sellImages[1]
  items[1].style.backgroundSize = '100% 100%'
} 

</script>

</body>





<!DOCTYPE html>

<head>

<style>
body {
  font-family: helvetica, sans-serif;
}
</style>

</head>

<body>
<h1>esha's restaurant</h1>

<div>
  <h2>welsh onion soko $14</h2>
<p>Mustard sierra leone bologi kale chard beet greens black-eyed pea sorrel amaranth garlic tigernut spring onion summer purslane asparagus lentil. </p>

<h2>pastrami boudin tongue $22</h2>
<p>Tri-tip capicola kielbasa salami brisket chicken rump strip steak drumstick. Meatloaf chuck boudin ribeye pork jowl. Andouille bacon jowl meatloaf pork loin prosciutto bresaola.</p>

<h2>fruitcake marzipan pudding dragee $8</h2>
<p>Lollipop tart cotton candy jelly-o carrot cake apple pie cupcake. Jelly-o bear claw ice cream candy canes.</p>
</body>*