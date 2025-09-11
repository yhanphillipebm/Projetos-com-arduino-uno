# 💡 Código Arduino – Botão e LED com Padrão de Piscar

## 📌 Objetivo
Esse programa tem como objetivo **controlar um LED no pino 13** através de um **botão no pino 2**, utilizando o resistor de pull-up interno do Arduino.  
Quando o botão é pressionado, o LED pisca em uma sequência programada.

---

## 🔌 Ligações do Circuito
- **LED**:  
  - Anodo (+) → Pino 13 do Arduino  
  - Catodo (–) → GND (com resistor de 220 Ω ou 330 Ω)  
- **Botão (push button)**:  
  - Um lado → Pino 2 do Arduino  
  - Outro lado → GND  
  - *(não precisa de resistor externo, pois o `INPUT_PULLUP` já ativa o resistor interno do Arduino)*  

---

## 💻 Código Completo
```cpp
int led = 13;   // Pino do LED
int btn = 2;    // Pino do botão
int tempo = 1000; // Tempo base (em ms)

void setup() {
  pinMode(led, OUTPUT);      // Define o LED como saída
  pinMode(btn, INPUT_PULLUP); // Botão com resistor interno pull-up
}

void loop() {
  int btnligado = digitalRead(btn); // Lê o estado do botão
  
  // Se o botão for pressionado (LOW porque pull-up inverte a lógica)
  if (btnligado == LOW) {

    // Pisca rápido 3 vezes
    for (int i = 0; i < 3; i++) {
      digitalWrite(led, HIGH);
      delay(tempo / 5);
      digitalWrite(led, LOW);
      delay(tempo / 5);
    }

    // Pausa curta
    delay(tempo / 5);

    // Acende o LED por 1 segundo
    digitalWrite(led, HIGH);
    delay(tempo);

    // Apaga o LED por 1 segundo
    digitalWrite(led, LOW);
    delay(tempo);
  }
}
```

---

## 📝 Explicação do Funcionamento
1. O **botão** é configurado com `INPUT_PULLUP`, então seu valor será:  
   - **HIGH** → quando não está pressionado.  
   - **LOW** → quando está pressionado.  

2. Quando o botão é pressionado, o LED faz a seguinte sequência:
   - **Pisca rápido 3 vezes** (0,2s ligado / 0,2s desligado).  
   - **Pausa curta**.  
   - **Fica ligado por 1 segundo**.  
   - **Fica desligado por 1 segundo**.  

3. O loop se repete sempre que o botão estiver pressionado.

---

## 🖼️ Representação do Fluxo
```text
Botão pressionado?
   └── NÃO → Nada acontece
   └── SIM → LED pisca 3x rápido → pausa → LED aceso 1s → LED apagado 1s
```

---

## 📖 Conclusão
Esse programa é uma ótima forma de:
- Praticar o uso de **for loops** no Arduino.  
- Aprender sobre **resistores pull-up internos**.  
- Criar **padrões personalizados de piscar LED** com base em botões.  

👉 Ele pode ser expandido para controlar **motores, buzzer ou até sinais luminosos mais complexos**.  
