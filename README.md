# pong.js
'1  '//variaveis da bolinha
let XBolinha = 100;
let YBolinha = 200;
let diametro = 20;
let raio = diametro/2;

//variaveis da velocidade
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

//variaveis da raquete
let XRaquete = 5;
let YRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 100;

//variaveis do oponente
let XRaqueteOponente = 585;
let YRaqueteOponente = 150;
let velocidadeYOponente; 


//placar do jogo
let meusPontos = 0;
let pontosdoOponente = 0;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(0);
 mostraBolinha();
 movimentaMinhaBolinha();
 verificaColisaoBorda();
  mostraRaquete(XRaquete,YRaquete);
  mostraRaquete(XRaqueteOponente,YRaqueteOponente);
  movimentaMinhaRaquete();
  verificaColisaoRaquete();
  movimentaRaqueteOponente();
  verificaColisaoRaqueteOponente();
  incluirPlacar();
  marcaPonto();
}

function mostraBolinha() {
  circle(XBolinha, YBolinha, diametro);
} 
function movimentaMinhaBolinha() {
  XBolinha += velocidadeXBolinha;
  YBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda() {
  if (XBolinha + raio > width || XBolinha - raio < 0) { velocidadeXBolinha *= -1}
   if (YBolinha + raio > height|| YBolinha - raio < 0) { velocidadeYBolinha *= -1}
}

function mostraRaquete(x,y){
rect(x,y,raqueteComprimento,raqueteAltura)
}

 function movimentaMinhaRaquete(){
  if(keyIsDown (UP_ARROW)){YRaquete -= 10;}
  if(keyIsDown (DOWN_ARROW)){YRaquete += 10;} 
}
 function verificaColisaoRaquete(){
  if (XBolinha - raio < XRaquete + raqueteComprimento 
   && YBolinha - raio < YRaquete + raqueteAltura
   && YBolinha + raio > YRaquete)
   {velocidadeXBolinha *=-1 } 
}
 
 function movimentaRaqueteOponente(){
  velocidadeYOponente = YBolinha - YRaqueteOponente - raqueteComprimento /2 - 30;
   YRaqueteOponente += velocidadeYOponente;
}
 function verificaColisaoRaqueteOponente() {
 if (XBolinha > XRaqueteOponente - raqueteComprimento 
    && YBolinha - raio < YRaqueteOponente + raqueteAltura
    && YBolinha + raio > YRaqueteOponente)
 {velocidadeXBolinha *= -1;}
 }
function incluirPlacar (){
  fill (255)
  text (meusPontos,278,26)
  text (pontosdoOponente,321,26)
}
function marcaPonto(){
  if (XBolinha > 590) {meusPontos += 1}
  if (XBolinha < 10) {pontosdoOponente +=1}
}
