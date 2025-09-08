# 📡 Protocolo HART (Highway Addressable Remote Transducer)

O **HART** é um protocolo de comunicação digital superposto ao sinal analógico de **4–20 mA**, bastante utilizado em instrumentação industrial.  
Ele surgiu como uma **evolução dos sistemas analógicos**, mantendo a compatibilidade com equipamentos já instalados, mas adicionando funcionalidades digitais.

---

## ⚙️ Contexto histórico

- Antigamente, o controle era feito por sistemas **pneumáticos** e depois por sistemas **analógicos em corrente (4–20 mA)**.  
- Esses sistemas tinham diversas **limitações**:
  - Dificuldade de configuração remota.
  - Incompatibilidade entre equipamentos de diferentes fabricantes.
  - Nenhum mecanismo de verificação de integridade do sinal.
  - Impossibilidade de atualizar firmware ou registrar alarmes.
  - Menor precisão no controle em malha fechada.

Para superar essas limitações, foi criado o **HART Protocol**, permitindo comunicação **digital + analógica** de forma simultânea.

---

## 🔗 Como funciona o HART?

- Baseado no modelo **Mestre/Escravo** (suporta até dois mestres).
- Comunicação **bidirecional**:  
  - O mestre envia comandos.  
  - O escravo (dispositivo de campo) responde com informações.  
- Utiliza a mesma fiação de **4–20 mA** já existente.
- Baseado no padrão **Bell 202 FSK (Frequency Shift Keying)**:
  - Sinal digital é sobreposto ao sinal analógico.  
  - Modulação em **FSK**:  
    - 1200 Hz representa bit `1`.  
    - 2200 Hz representa bit `0`.
  - Comunicação **half-duplex assíncrona** (um transmite por vez).
- Suporta operação em **ponto-a-ponto** e **multidrop** (vários dispositivos na mesma malha).

---

## 📋 Estrutura dos comandos HART

A troca de dados é feita através de **comandos**. Eles são classificados em três grupos:

1. **Universal Commands**  
   - Obrigatórios em todos os dispositivos HART.  
   - Permitem acesso a informações básicas:  
     - Leitura da variável primária (**PV – Primary Variable**) e suas unidades.  
     - Identificação do fabricante e versão do dispositivo.  
     - Status de comunicação.

2. **Common Practice Commands**  
   - Comandos opcionais, mas amplamente usados.  
   - Exemplos:  
     - Alterar o *range* de operação (ex.: 0–100 °C → –200 a 850 °C).  
     - Executar calibração remota.  
     - Teste de loop.

3. **Device-Specific Commands**  
   - Proprietários, definidos pelo fabricante.  
   - Usados para funções únicas, como calibrações avançadas e diagnósticos.  

---

## 🔧 Comissionamento HART

O comissionamento (configuração inicial) pode ser feito remotamente:  
- Definição de **tag**, **descritor** e **tipo de equipamento**.  
- Ajuste de **calibração** e **variação de leitura**.  
- Execução de **teste de loop** (calibração prática da malha 4–20 mA).  

---

## 📶 Camadas do Protocolo HART

### Camada Física
- Meio físico: par trançado até **3 km**.  
- Taxa de transmissão: **1.200 bps** (não 120 bps).  
- Transmissão assíncrona com estrutura semelhante ao **UART**:  
  - 1 start bit, 8 bits de dados, 1 bit de paridade, 1 stop bit.  
- Topologias: **barramento** ou **árvore**.  
- Mantém a compatibilidade com sinais analógicos de 4–20 mA.

### Camada de Enlace
- Garante a integridade da comunicação.  
- Controla a detecção de erros e o acesso ao meio.  

### Camada de Aplicação
- Define comandos, respostas, tipos de dados e relatórios de status.  

---

## 📂 DD – Device Description

- Arquivo de texto fornecido pelo fabricante, descrito em **DDL** ou **EDDL**.  
- Contém informações sobre parâmetros e características do dispositivo.  
- Permite que programadores portáteis ou sistemas supervisórios interpretem corretamente os dados de cada equipamento.

---

## ✅ Benefícios do HART

- Compatível com instalações **4–20 mA** já existentes.  
- Comunicação digital **não interfere** no sinal analógico.  
- Fácil de usar e entender.  
- Alta precisão e robustez.  
- Interoperável (vários fabricantes utilizam o padrão).  
- Suportado pela maioria dos dispositivos industriais modernos.

---

## 🌐 Relação com o Modelo OSI

O protocolo HART pode ser analisado segundo o modelo **OSI**:

- **Camada Física** → Fiação 4–20 mA + sinal digital FSK.  
- **Camada de Enlace** → Controle de acesso, detecção de erros.  
- **Camada de Aplicação** → Estrutura dos comandos e respostas HART.  

*(As demais camadas do OSI não são implementadas diretamente no HART, pois ele foi projetado como protocolo específico de automação).*

---

📌 **Próximos pontos para estudo**:
- Detalhar exemplos de **Common Practice Commands**.  
- Pesquisar lista oficial de **Universal Commands**.  
- Explorar como o **multidrop** altera a lógica de corrente na malha.  
- Descrever diferenças práticas entre HART e **Modbus**.
