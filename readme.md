# CHECKPOINT 1 EDGE COMPUTING - O CASO DA VINHERIA AGNELLO
## grupo: 

Descrição: Sistema de alarme que captura informações do ambiente e sinaliza se o ambiente está adequado para a preservação dos vinhos ou não.
<body>

## Índice
- <a href="#funcionalidades">Funcionalidades</a>
- <a href="#materiais">Materiais</a>
- <a href="#simulação">Simulação</a>
- <a href="#rodar">Como reproduzi-lo?</a>

## Funcionalidades

- [x] Identifica as portas, pinos de LED, buzzer e sensor LDR
- [x] Armazena valores lidos pelo sensor LDR
- [x] Inicializa a comunicação serial 
- [x] Realiza 10 leituras do sensor LDR, soma os valores e calcula a média, que representa a intensidade da luminosidade
- [x] Imprime a intensidade no monitor serial, e a  verifica
- [x] Acende os LEDS e o buzzer de acordo com os resultados da média.Se a intensidade for menor que 60, acende a luz verde, sinalizando que o ambiente é adequado. Se for maior que 60 e menor que 90, acende a luz amarela, sinalizando estado de alerta. Se a intensidade for maior que 90, acende a luz vermelha e o buzzer, sinalizando um problema.


## Simulação
[link da simulação](https://www.tinkercad.com/things/9yLRxcNCyDQ-copy-of-checkpoint-1-edge/editel?tenant=circuits) 👈


## Materiais 
</ol>
    <li> 1 placa de ensaio
    <li> 1 cabo USB 2.0 A/B
    <li> cabos jumper macho/macho
    <li> 1 LED difuso vermelho
    <li> 1 LED difuso verde
    <li> 1 LED difuso amarelo
    <li> 1 piezo buzzer 5V
    <li> 3 resistores de 100Ω
    <li> 1 fotoresistor LDR
    <li> 1 arduino UNO R3
    <li> 1 resistor de 200Ω
</ol>

## Como reproduzi-lo?

<strong>1- Instale o programa Arduino IDE [link para download](https://support.arduino.cc/hc/en-us/articles/360019833020-Download-and-install-Arduino-IDE) 👈

<hr>

<strong>2- Selecione os materiais e conecte-os na placa de ensaio da mesma forma que a imagem abaixo: <strong>

<img src="print.adr.png">

<hr>

<strong> 3- Conecte o cabo USB 2.0 A/B no arduino, a parte quadrada no arduino e o usb no computador/notebook. Acenderá um LED de on, informando que o arduino está ligado.

<hr>

<strong> 4- Entre no programa, clique em ferramentas, selecione o tipo de arduino e veja se o computador o reconheceu, logo abaixo em porta.
<img src="board.arduino.png">

<strong>5- Crie um novo arquivo e cole o código:

```
// Identificação das portas
int ledVerde = 4;		// Pino do LED verde
int ledAmarelo = 3;		// Pino do LED amarelo
int ledVermelho = 2;	        // Pino do LED vermelho
int buzzer = 5;		        // Pino do buzzer
int LDR = A0;			// Pino do sensor LDR (sensor de luminosidade)
	
int analogValue;		// Variável para armazenar o valor lido do sensor LDR

// Configurações iniciais
void setup() {
  pinMode(ledVerde,OUTPUT);		// Define o pino do LED verde como saída
  pinMode(ledAmarelo,OUTPUT);	// Define o pino do LED amarelo como saída
  pinMode(ledVermelho,OUTPUT);	// Define o pino do LED vermelho como saída
  pinMode(LDR, INPUT);			// Define o pino do sensor LDR como entrada
  pinMode(buzzer,OUTPUT);		// Define o pino do buzzer como saída

  Serial.begin(9600);			// Inicializa a comunicação serial com taxa de transferência de 9600 bps
  
  digitalWrite(buzzer, HIGH);	// Desliga o buzzer no início do programa
}

// Verificação do nível de luminosidade
void loop(){
  int temporario[10];			// Array temporário para armazenar valores de leitura do sensor LDR
  int soma = 0;					// Variável para armazenar a soma dos valores lidos do sensor LDR
  // Realiza 10 leituras do sensor LDR e soma os valores lidos
  for(int i = 0; i < 10; i++) {
    analogValue = analogRead(LDR);	// Realiza a leitura do sensor LDR
    soma += map(analogValue, 0, 255, 0, 100);	// Mapeia o valor lido para o intervalo de 0 a 100 e adiciona à soma  
  }

  int intensidade = soma / 10;		// Calcula a média das 10 leituras, representando a intensidade de luminosidade
  
 
  Serial.println(intensidade);		// Imprime a intensidade de luminosidade no monitor serial
  
  // Verifica a intensidade de luminosidade e ativa os LEDs e o buzzer de acordo com a necessidade
  if(intensidade < 60){  // Se a intensidade for menor que 60 (Baixa luminosidade - Ambiente adequado)
    digitalWrite(ledVerde, HIGH);	// Acende o LED verde
  }
  else if(intensidade >= 60 && intensidade <= 90){  // Se a intensidade estiver entre 60 e 90 (Luminosidade em nível de alerta)
    digitalWrite(ledAmarelo, HIGH);	// Acende o LED amarelo
  }
  else{   // Se a intensidade for maior que 90 (Alta luminosidade - Indicação de que há um problema)
    digitalWrite(ledVermelho, HIGH);// Acende o LED vermelho
    digitalWrite(buzzer, LOW);		// Liga o buzzer para indicar o problema
  }
  
  delay(3000);
  digitalWrite(ledVerde, LOW);	// Aguarda 3 segundos antes de reiniciar o loop
  // Desliga todos os LEDs e o buzzer antes de reiniciar o loop
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);
  digitalWrite(buzzer, HIGH);
}

```

<hr>

<strong>6- Após colado, clique na seta para enviar o código.

<hr>

<strong>7- Por fim, aguarde a compilação e envio do programa, depois abra o monitor serial para acompanhar o processo de leitura.
<img src="arduino.ide.png">

<strong>

</body>








