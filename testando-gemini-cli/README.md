# Ideia do Projeto

Para testar o **Gemini CLI**, será desenvolvido um jogo utilizando a stack **React, TypeScript, Vite, Yarn e SCSS**.

---

## O Jogo

O jogo que o modelo deve criar é o seguinte:

- O jogo se passa em uma **grid 6x6**.  
- É para **2 jogadores na mesma máquina**, intercalando turnos.  
- Mistura **cartas** com **tabuleiro**.  
- As cartas afetam o tabuleiro ao serem jogadas.  
- Existem **2 baralhos**:  
  - Cartas de **energia**.  
  - Cartas **jogáveis** (magias e personagens).  
- **Baralho de Energia**: possui cartas com valores de **1, 2 e 3 energias**.  
- **Baralho de Cartas Jogáveis**:  
  - **Personagens** → peças na grid.  
  - **Magias** → efeitos no tabuleiro.  
- **Personagens**:  
  - Podem **andar 1 espaço** por turno ou **atacar 1 vez** por turno.  
  - Cada personagem só pode realizar **1 ação por turno**.  
  - Possuem **alcance** de 1, 2 ou 3 quadrados (horizontal/vertical).  
- **Fluxo de turno**:  
  - O jogador puxa **2 cartas de energia** e escolhe **1**.  
  - Essa carta vai para seu **estoque de energia** (máx. 3 cartas).  
  - O jogador sempre terá **5 cartas na mão**; deve comprar até completar 5.  
- **Restrições**:  
  - Personagens só podem ser jogados na **própria metade** do campo.  
  - Só é possível atacar **personagens adversários**.  
- **Atributos das cartas**:  
  - **Personagem** → custo, dano, vida (HP), alcance.  
  - **Magia** → custo, dano e alcance (todas as direções).  
- **Energia**:  
  - Deve-se **descartar cartas do estoque** de energia para pagar o custo.  

---

## Refinamento feito por LLM (Gemini 2.5 Pro)

### Ideia Refinada: Projeto **"Grid Clash"**

Um jogo de **estratégia tática em turnos**, para dois jogadores locais, construído com **React, TypeScript, Vite, Yarn e SCSS**.  
Objetivo: testar a capacidade do **Gemini CLI** em criar um jogo funcional com regras claras.

---

### Conceito Central

- Dois jogadores se enfrentam em um tabuleiro **6x6**.  
- Cada jogador usa cartas de **personagem** e **magia** para controlar o campo.  
- O recurso principal é a **Energia**, usada para jogar cartas.  
- O jogo termina quando um jogador derrota todos os personagens do adversário.  

---

### Mecânicas Detalhadas

#### 1. O Tabuleiro e Condição de Vitória
- **Grid**: 6x6.  
- **Zonas Iniciais**: 2 primeiras fileiras de cada lado → zona de invocação.  
- **Objetivo**: eliminar todos os personagens inimigos.  

#### 2. Sistema de Recursos: Energia
- **Banco de Energia**: até 3 cartas.  
- **Baralho de Energia**: cartas de valor 1, 2, 3.  
- **Início do Turno**:  
  - Comprar 2 cartas de energia.  
  - Escolher 1 para o banco (se houver espaço).  
  - Descartar a outra.  
- **Gasto de Energia**: descartar cartas que somem o custo da carta jogada.  
  - Exemplo: custo 3 → usar uma carta "3" ou "1 + 2".  

#### 3. Sistema de Cartas e Mão
- **Baralho de Jogo**: único de cada jogador.  
- **Mão**: sempre 5 cartas.  
- **Compra**: no início do turno, compra até ter 5.  

#### 4. Estrutura do Turno
1. **Fase de Manutenção**  
   - Comprar energia (2 → escolhe 1).  
   - Comprar cartas até 5.  
   - Personagens recuperam 1 ponto de ação.  

2. **Fase Principal**  
   - Jogar personagens (pagando custo, colocando em zona própria).  
   - Jogar magias (pagando custo, aplicando efeito).  

3. **Fase de Ação**  
   - Cada personagem pode **mover** (1 casa) ou **atacar** (dentro do alcance).  
   - Jogador pode encerrar turno a qualquer momento.  

#### 5. Tipos de Cartas
- **Personagens**:  
  - Atributos: custo, vida (HP), dano, alcance (1–3 em linha reta).  

- **Magias**:  
  - Atributos: custo, efeito/dano, área de efeito.  
  - Tipos de AoE:  
    - Alvo único.  
    - Área em volta (ex: 3x3).  
    - Linha reta.  

---

### Escopo para o MVP (Produto Mínimo Viável)

**Interface e Tabuleiro**  
- Grid 6x6 renderizado.  
- Zonas de invocação destacadas.  
- Exibição de mão, energia e baralhos.  

**Lógica do Jogo**  
- Turnos alternados.  
- Fluxo completo de turno.  
- Jogar personagens e magias.  
- Ações: mover/atacar.  
- Verificação de vitória.  

**Conteúdo Inicial**  
- **Personagens**:  
  - **Guerreiro** → custo 2, 3 HP, 2 dano, alcance 1.  
  - **Arqueiro** → custo 3, 2 HP, 2 dano, alcance 3.  
- **Magia**:  
  - **Bola de Fogo** → custo 2, 2 dano, alvo único, alcance 3.  
- **Baralho de Energia**: valores 1, 2, 3.  

## Refinamento feito por LLM (ChatGPT WebUI Free - 2025.08.21)

# Ideia do Projeto  

O objetivo é **testar o Gemini CLI** desenvolvendo um jogo utilizando a stack **React, TypeScript, Vite, Yarn e SCSS**.  

## O Jogo  

Trata-se de um jogo de **tabuleiro digital 6x6 com cartas**, projetado para **2 jogadores locais**, que jogam intercalando turnos.  

### Mecânicas principais  

- **Turnos alternados**: cada jogador realiza suas ações e passa a vez.  
- **Cartas + Tabuleiro**:  
  - **Cartas de energia** alimentam o sistema de custo.  
  - **Cartas jogáveis** são divididas em **personagens** (peças de tabuleiro) e **magias** (efeitos pontuais).  

### Estrutura de cartas  

#### 1. Cartas de Energia  
- Valores possíveis: **1, 2 ou 3 energias**.  
- O jogador compra **2 cartas de energia por turno** e mantém apenas **1 no estoque**.  
- Estoque máximo: **3 cartas**.  

#### 2. Cartas Jogáveis  
- O jogador sempre mantém **5 cartas na mão**; no início do turno compra até completar 5.  
- Tipos:  

**Personagens**  
- Colocados apenas na **metade do campo do jogador**.  
- Atributos: **custo**, **dano**, **defesa**, **range de ataque**.  
- Ações possíveis (1 por turno): **mover 1 espaço** ou **atacar**.  
- Alcance: **1, 2 ou 3 quadrados** (horizontal ou vertical).  

**Magias**  
- Atributos: **custo**, **dano**, **alcance total** (todas as direções).  
- Aplicam efeitos diretamente na grid.  

### Regras de energia e custo  

- Para jogar qualquer carta (personagem ou magia), o jogador deve **descartar cartas de energia do estoque** equivalentes ao custo.  

### Objetivo do jogo  

- Ainda não definido, podendo ser:  
  - **Eliminar todas as peças adversárias**.  
  - **Controlar determinado número de espaços do tabuleiro**.  
