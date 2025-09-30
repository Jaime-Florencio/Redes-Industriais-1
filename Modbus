# 📘 Modbus

## 🔹 O que é?
- Protocolo de comunicação industrial criado em 1979 pela Modicon.
- Permite **troca de dados** entre dispositivos como CLPs, sensores, IHMs, inversores, medidores.
- É uma **linguagem comum** para equipamentos de diferentes fabricantes.

---

## ⚙️ Como funciona?
- Estrutura **Mestre–Escravo** (ou Cliente–Servidor):
  - **Mestre:** envia pedidos (ex.: CLP, supervisório).
  - **Escravo:** responde aos pedidos (ex.: sensor, inversor).

📌 Fluxo:  
Mestre → Requisição → Escravo → Resposta

---

## 🔌 Tipos de Modbus
1. **Modbus RTU**  
   - Comunicação serial (RS-485/232).  
   - Dados em binário → mais rápido.  

2. **Modbus ASCII**  
   - Também serial, mas envia em ASCII (mais lento).  

3. **Modbus TCP/IP**  
   - Usa Ethernet (rede de computadores).  
   - Baseado em TCP/IP → fácil integração.

---

## 🧩 Estrutura da mensagem
1. Endereço do escravo.  
2. Código de função (ler, escrever, etc.).  
3. Dados (valores ou endereços).  
4. Verificação de erro (CRC ou checksum).  

---

## 📊 Áreas de memória
- **Coils:** saídas digitais (liga/desliga).  
- **Discrete Inputs:** entradas digitais (somente leitura).  
- **Input Registers:** entradas analógicas (somente leitura).  
- **Holding Registers:** variáveis de leitura/escrita (setpoints, parâmetros).  

---

## 🛠️ Como montar a comunicação
1. Definir Mestre e Escravo.  
   - Exemplo: CLP (mestre) lê sensor (escravo).  
2. Escolher tipo (RTU, ASCII, TCP/IP).  
3. Configurar parâmetros.  
   - Serial: baud rate, paridade, stop bits.  
   - TCP: IP e porta 502.  
4. Mapear endereços.  
   - Cada escravo tem endereço único.  
   - Cada variável está em um registrador.  
5. Testar a comunicação.  
   - Softwares: ModScan, Modbus Poll, SCADA.  

---

## ✅ Vantagens
- Simples de implementar.  
- Muito difundido.  
- Aberto e sem licença.  
- Funciona em ambientes industriais.  

---

## ❌ Desvantagens
- Velocidade limitada (RTU).  
- Escravos não iniciam comunicação.  
- Sem segurança nativa (sem criptografia).  
- Não ideal para redes muito grandes.  

---

# 📘 Endereços no Modbus

## 🔹 Conceito básico
- Se temos **N bits** para representar um endereço, o limite é:
  
Total de endereços = 2^N


- Exemplo:  
- 2 bits → 2² = **4 endereços possíveis** (00, 01, 10, 11).  
- 3 bits → 2³ = **8 endereços possíveis**.  
- 8 bits → 2⁸ = **256 endereços possíveis**.

---

## 🔹 Endereço de escravo no Modbus
- Cada dispositivo escravo possui um **endereço de 1 byte (8 bits)**.  
- Intervalo possível: 0 a 255.  
- Mas, por padrão, o Modbus usa:  

- **1 a 247** → endereços válidos para escravos.  
- **0** → reservado para mensagens broadcast.  
- **248 a 255** → reservados para funções especiais.

👉 Portanto: até **247 escravos** podem existir em uma mesma rede Modbus.

---

## 🔹 Endereço de registradores
Dentro de cada escravo existem **registradores** (áreas de memória para variáveis).

- Endereço do registrador usa **16 bits**.  
- Intervalo possível: 0 a 65.535.  
- Logo, cada tabela (Coils, Discrete Inputs, Holding Registers, Input Registers) pode ter até **65.536 posições**.

---

## 📊 Resumo em tabela

| Campo                  | Bits usados | Intervalo possível   | Limite prático no Modbus |
|-------------------------|-------------|----------------------|---------------------------|
| Endereço do escravo     | 8 bits      | 0 – 255              | 1 – 247 (válidos)         |
| Endereço do registrador | 16 bits     | 0 – 65.535           | até 65.536 posições       |

---

## ✅ Conclusão
- A regra geral é: **2^N valores possíveis** para N bits.  
- No Modbus:  
- Escravos → 8 bits → até 247 dispositivos válidos.  
- Registradores → 16 bits → até 65.536 posições por tabela.  


# 📘 Registradores no Modbus

## 🔹 O que são?
- Registradores são **posições de memória** dentro do dispositivo escravo.  
- Cada registrador tem um **endereço** e guarda um **valor** (normalmente 16 bits = 2 bytes).  
- O mestre acessa os registradores para **ler informações** ou **escrever comandos**.

---

## 🔹 Tipos de registradores
O Modbus organiza os dados em **tabelas**:

1. **Coils (0xxxx)**  
   - 1 bit, leitura/escrita.  
   - Exemplo: ligar/desligar uma saída digital.  

2. **Discrete Inputs (1xxxx)**  
   - 1 bit, somente leitura.  
   - Exemplo: estado de um sensor (ON/OFF).  

3. **Input Registers (3xxxx)**  
   - 16 bits, somente leitura.  
   - Exemplo: valor de temperatura medido.  

4. **Holding Registers (4xxxx)**  
   - 16 bits, leitura/escrita.  
   - Exemplo: setpoint de velocidade de motor.  

---

## 🔹 O que eles fazem?
- **Guardam valores de sensores:**  
  Sensor mede → valor vai para o registrador → mestre lê.  

- **Recebem comandos do mestre:**  
  Mestre escreve no registrador → escravo executa ação → atua em motor/válvula.  

---

## 🔹 Exemplo prático (inversor de frequência)
- Registrador **40001** → Setpoint de velocidade (holding).  
- Registrador **30001** → Velocidade atual (input).  
- Registrador **00001** → Liga/desliga motor (coil).  

📌 Fluxo:
1. Mestre escreve em **40001** → define velocidade desejada.  
2. Mestre lê **30001** → verifica velocidade real.  
3. Mestre escreve em **00001** → liga o motor.  

---

## 📝 Resumindo
- Registrador = **caixinha de memória** do escravo.  
- Guarda dados de sensores ou comandos.  
- Mestre usa registradores para **monitorar** (ler) ou **controlar** (escrever).  
