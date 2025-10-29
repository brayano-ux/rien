
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shopping</title>
    <style>
        body{
            background-color: white;
       

        }
        h2{
            color: blue;
            text-align: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-size: 25px;
            text-decoration: double;
            box-shadow: 2px -1px 4px rgba(1, 0,1,1, 0);
        }
        h3{
            color: blue;
            text-align: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            font-size: 25px;
            text-decoration: double;
            box-shadow: 2px -1px 4px rgba(1, 0,1,1, 0);
        }
        p{
            text-align: center;
            text-emphasis: none;
            text-transform: capitalize;
            text-shadow: 0cap;
            text-overflow: clip;
            text-size-adjust: 25px;
            font-size: 20px;
            font-family: Georgia, 'Times New Roman', Times, serif;
            
        }
        img{
            border: 2px solid transparent;
            width: 200px;
            height: 200px;
            border-radius: 10px;
            transition: all;
            transition: transform 0.2s;
            filter: brightness(1.2);
            box-shadow: 0 0 10 px rgb(red, green, blue);
            cursor: pointer;
           
        }
        img:focus{
            border: 2px solid red;
            outline: none;
        }
       img:hover{
        transform: scale(1.1);
       }
       .shopping{
        background-color: white;
    padding: 20px;
    margin: 20px auto;
    border-radius: 10px;
    width: 100%;
    height: 100%;
    max-width: 1000px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    position: relative;
    display: flex;flex-wrap: wrap;justify-content: space-around;
    
       }
       .pantalon{
        background-color: whitesmoke;
    padding: 20px;
    margin: 20px auto;
    border-radius: 10px;
    width: 100%;
    height: 100%;
    max-width: 1000px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    position: relative;
    display: flex;flex-wrap: wrap;justify-content: space-around;
       }
       .sacs{
        background-color: beige;
    padding: 20px;
    margin: 20px auto;
    border-radius: 10px;
    width: 100%;
    height: 100%;
    max-width: 1000px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    position: relative;
    display: flex;flex-wrap: wrap;justify-content: space-around;
       }
       span{
        font-size: 25px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        color: blue;
       
       }
       #total{
        text-align: right;
        font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
        font-size: 25px;
       }
       .commande{
        height: 50px;
        width: 40%;
        text-align: center;
        font-size: 25px;
        border-radius: 15px;
        background-color: green;
       }
       #annuler{
        height: 50px;
        width: 40%;
        text-align: center;
        font-size: 25px;
        border-radius: 15px;
        background-color: red;
       }
       .whatsapp{
        background-color: white;
    padding: 20px;
    margin: 20px auto;
    border-radius: 10px;
    width: 100%;
    height: 100%;
    max-width: 1000px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    position: relative;
       }
       input{
        border-radius: 10px;
        height: 30px;
        width: 30%;
       }
       label{
        font-size: 20px;
        color: blue;
        font-family: Verdana, Geneva, Tahoma, sans-serif;
       }
       .menu{
        height: 50px;
        width: 100px;
        background-color: aqua;
        border-radius: 15px;
        position: fixed;left: 0px;top: 10px;
        font-size: 1.2rem;
        transition: background-color 0.3s ease, transform 0.2s ease;
        

       }
    </style>
</head>
<body>
 <h2>BIENVENUE DANS LE SHOPPING LA GRACE</h2> 
 <br>
 <p> <strong>Le shopping GRACE</strong> vous presentes une collection de vetements de haute qualite <br> qui valorisent le style  maxulin <br>et femini dans un esprit elegant et positif</p>
 <button class="menu"  id="menu">Menu Principal</button>
 <form action="" id="whatsappform">
 <h3>HAUT</h3>  
 <div class="shopping">
 <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000','https://i.postimg.cc/ZKLSgJmQ/IMG-20250625-WA0026.jpg')">
 <img src="c:\Users\lenovo\Pictures\1000006999.jpg" alt="">
 <br>
 <span>T-shirt  prix= 6000 fcfa</span>
</div>
<div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000007014.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000008002.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000015507.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000023478.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000023444.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000023422.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000022141.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('T-shirt','6000')">
    <img src="c:\Users\lenovo\Pictures\1000020460.jpg" alt="">
    <br>
 <span>T-shirt  prix= 6000 fcfa</span>
   </div>
</div>
<br>
<br>
<h3>PANTALON</h3>  
<br>
<div class="pantalon">
    <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Pantalon','5000','https://i.postimg.cc/bYHWYL5D/IMG-20250310-WA0019.jpg')">
        <img src="c:\Users\lenovo\Pictures\1000023300.jpg" alt="">
        <br>
     <span>Pantalon  prix= 5000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Pantalon','5000')">
        <img src="c:\Users\lenovo\Pictures\1000052287.jpg" alt="">
        <br>
     <span>Pantalon  prix= 5000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Pantalon','5000')">
        <img src="c:\Users\lenovo\Pictures\1000056987.jpg" alt="">
        <br>
     <span>Pantalon  prix= 5000 fcfa</span>
       </div>
</div>
       <br>
<br>
<h3>SACS</h3>  
<br>
<div class="sacs">
    <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000039947.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000044781.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000057660.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000057651.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000057633.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
       <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Sacs','4000')">
        <img src="c:\Users\lenovo\Pictures\1000055136.jpg" alt="">
        <br>
     <span>Sacs  prix= 4000 fcfa</span>
       </div>
</div>
<br>
<br>
<h3>CHAUSSURES</h3>
<br>
<div class="sacs">
<div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures','3000','https://i.postimg.cc/mgr05M8c/IMG-20250310-WA0049.jpg')">
 <img src="c:\Users\lenovo\Pictures\1000038903.jpg" alt="">
 <br>
<span>Chaussures  prix:3000 fcfa</span>
</div>
<div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures','3000')">
    <img src="c:\Users\lenovo\Pictures\1000041454.jpg" alt="">
    <br>
   <span>Chaussures  prix:3000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures','3000')">
    <img src="c:\Users\lenovo\Pictures\1000041445.jpg" alt="">
    <br>
   <span>Chaussures  prix:3000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures',3000)">
    <img src="c:\Users\lenovo\Pictures\1000039873.jpg" alt="">
    <br>
   <span>Chaussures  prix:3000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures',3000)">
    <img src="c:\Users\lenovo\Pictures\1000040729.jpg" alt="">
    <br>
   <span>Chaussures  prix:3000 fcfa</span>
   </div>
   <div style="width: 23.33%;margin: 10px;" class="" onclick="habit('Chaussures',3000,'https://i.postimg.cc/mgr05M8c/IMG-20250310-WA0049.jpg')">
    <img src="c:\Users\lenovo\Pictures\1000039202.jpg" alt="">
    <br>
   <span>Chaussures  prix:3000 fcfa</span>
   </div>
</div> 
<div class="whatsapp">
   
    <label for="">EntrezVotre Nom:</label>
    <br>
    <br>
    <input type="text" id="nome" placeholder="Entrez votre Nom" required>
    <br>
    <br>
    <label for="">Entrez l,heure de Retrait:</label>
    <br>
    <br>
    <input id="temps" type="time" placeholder="Enterz L,heure de Retrait" required>
    <br>
    <br>
<div id="total">Total : <span id="totalPrice">0</span> FCFA</div>
<button class="commande" type="submit" > Commander via WhatsApp</button>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<button id="annuler" type="reset">Annuler la commande</button>
<span id="totale" style="display: none;"> total:</span>
</div>
</form>
<script>
let total = 0;
let panier = [];

const nomInput = document.getElementById('nome');
const tempsInput = document.getElementById('temps');
const messForm = document.getElementById('whatsappform');
function habit(nom, prix, image) {
  panier.push({ nom, prix, image });
  total += prix;
  alert(`${nom} 👜 ajouté au panier 🧦`);
  
  document.getElementById('totale').textContent = total;
  document.getElementById('total').textContent = `Total = ${total} FCFA`;
}


messForm.addEventListener('submit', (e) => {
  e.preventDefault();
  const nom = nomInput.value.trim();
  
  if (panier.length === 0) {
    alert("🛒 Votre panier est vide !");
    return;
  }

  let message = `Bonjour 👏 je m'appelle ${nom}, je souhaite commander :\n`;
  let totalCommande = 0;
  panier.forEach(item => {
    message += `- ${item.nom} = ${item.prix} FCFA\n📷 Image : ${item.image}\n`;
    totalCommande += item.prix;
  });
  message += `\n🧾 Total : ${totalCommande} FCFA`;
  message += `\n🕒 Heure de retrait : ${tempsInput.value}`;
  message += `\n🙏 Merci d'avance !`;

  const numero = '237657300644';
  const lien = `https://wa.me/${numero}?text=${encodeURIComponent(message)}`;
  window.open(lien, '_blank');
});

messForm.addEventListener('reset', (e) => {
  e.preventDefault();
  const nom = nomInput.value.trim();
  const numero = '237657300644';
  
  if (!nom) {
    alert("Veuillez entrer votre nom avant d'annuler la commande.");
    return;
  }
  
  const messa = `${nom} annule sa commande. Désolé pour le dérangement.`;
  const lien = `https://wa.me/${numero}?text=${encodeURIComponent(messa)}`;
  window.open(lien, '_blank');
});
document.getElementById("menu").addEventListener("click",function(){
window.location.href="file:///C:/Users/lenovo/Documents/photo%20de%20profil.html";
});
</script>
</body>
