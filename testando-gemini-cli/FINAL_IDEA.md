# Por Gemini 2.5 Pro

# Ideia Unificada: Projeto "Grid Clash"

## 1. Sinopse do Projeto
Grid Clash é um jogo de estratégia tática em turnos para dois jogadores locais, desenvolvido com a stack **React, TypeScript, Vite, Yarn e SCSS**. O projeto tem como objetivo principal testar e demonstrar a capacidade do **Gemini CLI** na criação de um jogo funcional e com regras bem definidas.

## 2. Conceito Central do Jogo
Dois jogadores se enfrentam em um **tabuleiro 6x6**, utilizando baralhos de cartas para invocar personagens e lançar magias. O gerenciamento de um recurso chamado **Energia** é fundamental para executar ações.  
A condição de vitória é simples e direta: **eliminar todos os personagens do adversário**.

## 3. Mecânicas Detalhadas

### A. O Tabuleiro e Condição de Vitória
- **Grid**: Tabuleiro de 6x6.  
- **Zonas de Invocação**: As duas primeiras fileiras de cada jogador são sua zona de invocação. Personagens só podem ser colocados nessas áreas.  
- **Objetivo**: O jogo termina quando um jogador não tiver mais nenhum personagem no tabuleiro.  

### B. Sistema de Recursos: Energia
- **Baralho de Energia**: Um baralho separado com cartas de valor **1, 2 e 3**.  
- **Estoque de Energia**: O jogador pode armazenar no máximo **3 cartas de energia**.  
- **Geração de Energia**: No início de cada turno, o jogador compra **2 cartas do baralho de energia**, escolhe **1 para adicionar ao estoque** (se houver espaço) e descarta a outra.  
- **Gasto de Energia**: Para jogar uma carta (Personagem ou Magia), o jogador deve **descartar cartas de seu estoque cuja soma seja igual ou maior que o custo da carta jogada**.  

### C. Sistema de Cartas Jogáveis
- **Baralho de Jogo**: Cada jogador possui seu próprio baralho com cartas de **Personagem** e **Magia**.  
- **Mão do Jogador**: O jogador sempre mantém uma mão de **5 cartas jogáveis**.  
- **Compra de Cartas**: No início de seu turno, após a fase de energia, o jogador compra cartas do seu baralho de jogo até ter **5 na mão**.  

### D. Estrutura do Turno
O turno de um jogador é dividido em fases claras:

#### Fase de Manutenção (Início do Turno)
- **Recuperação**: Todos os personagens do jogador no tabuleiro recuperam seu ponto de ação, podendo agir novamente neste turno.  
- **Compra de Energia**: O jogador compra 2 cartas de energia, escolhe 1 para o estoque e descarta a outra.  
- **Compra de Cartas**: O jogador compra cartas jogáveis até completar a mão de 5 cartas.  

#### Fase Principal (Ações do Jogador)
O jogador pode realizar as seguintes ações em qualquer ordem e quantas vezes puder pagar os custos:  
- **Jogar um Personagem**: Pagar seu custo de energia e posicioná-lo em um espaço vazio na sua zona de invocação.  
- **Jogar uma Magia**: Pagar seu custo de energia e aplicar seu efeito no alvo designado.  
- **Usar Ações de Personagens**: Comandar cada personagem no tabuleiro para realizar uma ação (Mover ou Atacar).  

#### Fase Final (Fim do Turno)
- O jogador passa a vez para o oponente.  

### E. Tipos de Cartas e Atributos

#### Personagens
Peças que ocupam o tabuleiro.  

**Atributos**:  
- **Custo**: Energia necessária para jogar a carta.  
- **Vida (HP)**: Pontos de dano que o personagem pode sofrer antes de ser removido.  
- **Dano**: Pontos de dano que o personagem causa ao atacar.  
- **Alcance (Range)**: A distância máxima (em quadrados, apenas horizontal/vertical) que o personagem pode atacar.  

**Ações (1 por turno)**:  
- **Mover**: Deslocar-se 1 quadrado em qualquer direção (horizontal ou vertical).  
- **Atacar**: Causar dano a um personagem adversário dentro do seu alcance.  

#### Magias
Efeitos instantâneos no tabuleiro.  

**Atributos**:  
- **Custo**: Energia necessária para jogar a carta.  
- **Efeito**: O que a magia faz (ex: causar dano).  
- **Alcance**: A distância máxima para lançar a magia.  
- **Área de Efeito (AoE)**: Como o efeito é distribuído (ex: alvo único, área 3x3, linha reta).  

## 4. Escopo para o MVP (Produto Mínimo Viável)

### Interface e Componentes Visuais
- Renderização do grid 6x6.  
- Visualização da mão de cartas, estoque de energia e baralhos de cada jogador.  
- Destaque visual para zonas de invocação, alcance de movimento e ataque.  

### Lógica Fundamental do Jogo
- Sistema de turnos alternados.  
- Implementação completa do fluxo de turno (manutenção, principal, final).  
- Lógica para jogar personagens e magias pagando custos de energia.  
- Implementação das ações de personagem: Mover e Atacar.  
- Sistema de dano, HP e remoção de personagens.  
- Verificação da condição de vitória.  

### Conteúdo Inicial (Hardcoded)
- **Personagens (2)**:  
  - **Guerreiro**: Custo 2, 3 HP, 2 Dano, Alcance 1.  
  - **Arqueiro**: Custo 3, 2 HP, 2 Dano, Alcance 3.  
- **Magia (1)**:  
  - **Bola de Fogo**: Custo 2, 2 Dano, Alvo Único, Alcance 3.  
- **Baralho de Energia**: Composto por cartas de valor **1, 2 e 3**.  

# Por ChatGPT WebUI Free - 2025.08.21

# Grid Clash — Especificação Unificada (MVP)

## 1) Objetivo do projeto
Validar o Gemini CLI gerando um jogo completo (stack React + TypeScript + Vite + Yarn + SCSS) com regras claras, estado previsível e testes básicos.

## 2) Visão do jogo
- Jogo tático em turnos para 2 jogadores locais em um tabuleiro 6x6.  
- Cartas jogáveis (personagens e magias) interagem com o tabuleiro.  
- Cartas de energia formam o sistema de custo.  

**Condição de vitória (MVP):** vence quem eliminar todas as unidades do oponente.

## 3) Campo e zonas
- **Grid:** 6x6, coordenadas (linha 0–5, coluna 0–5).  

**Zonas de invocação:**  
- Jogador A: linhas 0 e 1.  
- Jogador B: linhas 4 e 5.  

**Spawn:** personagens só podem entrar na própria metade (linhas 0–2 para A; 3–5 para B) e preferencialmente na zona (0–1 ou 4–5).  
(Regra simples para MVP: permitir em toda a metade; destacar visualmente a zona de invocação como “ideal”.)

## 4) Recursos: Energia
- **Baralho de Energia:** cartas de valor 1, 2, 3 (quantidade suficiente para a partida; reembaralha quando esgota).  
- **Banco de Energia:** até 3 cartas.  
- **Início de turno:** comprar 2 do baralho de energia → guardar 1 no banco (se houver espaço) e descartar 1.  
- **Pagamento de custo:** descartar cartas do banco cuja soma ≥ custo (excesso é perdido).  

## 5) Mão e compra
- **Baralho Jogável:** cada jogador tem o seu (personagens + magias).  
- **Mão:** manter sempre 5 cartas (comprar no início do turno até completar 5; reembaralhar descarte quando necessário).  
- **Limites (MVP):** sem limites de cópia por carta além da lista inicial.  

## 6) Tipos de carta e atributos

### 6.1 Personagens
- **Atributos:** custo, HP, dano, alcance.  
- **Ações (1 por turno):** mover 1 casa (ortogonal) ou atacar.  
- **Alcance de ataque:** 1–3 casas em linha reta (horizontal/vertical).  
- Sem bloqueio de linha de visão no MVP.  
- **Empate de ocupação:** não pode entrar em célula ocupada; morte remove a peça.  

### 6.2 Magias
- **Atributos:** custo, efeito/dano, alcance (em todas as direções, distância medida por Chebyshev no MVP).  
- **Tipos (MVP):** alvo único. (Deixar 3x3/linha reta como expansão futura.)  

## 7) Estrutura do turno

**Manutenção**  
- Comprar 2 energias → guardar 1 (se houver espaço), descartar 1.  
- Comprar cartas jogáveis até ter 5 na mão.  
- Remover marcadores temporários (se existirem no futuro).  

**Principal**  
- Jogar personagens (pagar custo; colocar na metade própria).  
- Jogar magias (pagar custo; aplicar efeito).  

**Ação**  
- Para cada personagem do jogador: mover 1 ou atacar 1 vez.  

**Encerrar turno**  
- Passar a vez; checar condição de vitória.  

## 8) Conteúdo inicial (MVP)

**Personagens**  
- **Guerreiro** — custo 2, HP 3, dano 2, alcance 1.  
- **Arqueiro** — custo 3, HP 2, dano 2, alcance 3.  

**Magias**  
- **Bola de Fogo** — custo 2, 2 de dano, alvo único, alcance 3 (todas as direções).  

**Energia**  
- Valores 1, 2, 3 (distribuição simples, ex.: 12×1, 8×2, 6×3 por jogador no MVP).  

## 9) Regras de colisões e bordas (MVP)
- **Movimento:** apenas ortogonal; não atravessa peças; não entra em célula ocupada.  
- **Ataque:** seleciona alvo inimigo dentro do alcance em linha reta; aplica dano; HP ≤ 0 remove a unidade.  
- **Empate de compra:** se o baralho acabar, reembaralhar descarte e continuar.  
- **Sem turnos mortos:** se não puder agir, o jogador apenas encerra o turno.  

## 10) Interface (MVP)
- Tabuleiro 6x6 com destaque de metades e zonas.  
- Mão (5 cartas) e Banco de Energia (até 3) com somatório visível.  
- Painel de Ações (jogar carta, mover, atacar, encerrar turno).  
- Realces de alcance ao selecionar peça/carta.  
- Log de combate minimalista (texto).  
- Indicador de turno.  

## 11) Modelo de dados (TypeScript, guia)
```ts
type PlayerId = 'A' | 'B';

type EnergyCard = { id: string; value: 1 | 2 | 3; };
type Range = 1 | 2 | 3;

type CharacterCard = {
  id: string;
  name: 'Guerreiro' | 'Arqueiro';
  type: 'character';
  cost: number;
  hp: number;
  atk: number;
  range: Range; // linha reta (ortogonal)
};

type SpellCard = {
  id: string;
  name: 'Bola de Fogo';
  type: 'spell';
  cost: number;
  damage: number;
  range: Range; // Chebyshev (todas as direções)
  target: 'unit'; // MVP
};

type PlayableCard = CharacterCard | SpellCard;

type Cell = { row: number; col: number; };
type Unit = {
  id: string;
  owner: PlayerId;
  cardRef: 'Guerreiro' | 'Arqueiro';
  hp: number;
  pos: Cell;
  actedThisTurn: boolean;
};

type GameState = {
  turn: PlayerId;
  board: (Unit | null)[][];
  hands: Record<PlayerId, PlayableCard[]>;
  banks: Record<PlayerId, EnergyCard[]>; // energia
  decks: {
    energy: Record<PlayerId, EnergyCard[]>;
    playable: Record<PlayerId, PlayableCard[]>;
    discard: Record<PlayerId, PlayableCard[]>;
  };
  winner: PlayerId | null;
};
```

## 12) Lógica essencial (pseudo)

- **Pagar custo**: selecionar cartas do banco com soma ≥ custo → descartar; excesso perdido.  
- **Invocar personagem**: validar metade, célula livre → criar Unit com hp do card.  
- **Magia (Bola de Fogo)**: validar alvo em alcance Chebyshev ≤ 3 → aplicar 2 de dano.  
- **Mover**: validar célula ortogonal adjacente livre → atualizar pos.  
- **Atacar**: alvo inimigo em linha reta com distância ≤ range → aplicar atk.

## 13) Backlog do MVP (ordem sugerida)

- Projeto base (Vite + React + TS + SCSS) e estado global (Zustand ou Redux; Zustand é mais leve).  
- Modelo de dados + embaralhamento determinístico (seed para testes).  
- Render do tabuleiro e das mãos/banco de energia.  
- Fluxo de turno completo (manutenção → principal → ação → fim).  
- Ações: jogar personagem, mover, atacar, jogar magia.  
- Condição de vitória + tela de fim de jogo.  
- Realces de alcance e validações (UX mínima).  
- Log de ações (texto).  
- Testes de regras críticas (pagamento, alcance, morte, vitória).

## 14) Critérios de aceitação (MVP)

- É possível iniciar partida, alternar turnos e concluir uma partida por eliminação total.  
- Pagamento de energia funciona com soma ≥ custo; banco respeita limite 3.  
- Mão mantém 5 cartas; baralhos reembaralham quando esgotam.  
- Personagens movem 1 ou atacam (exclusivo por turno).  
- Alcances respeitados (personagem: ortogonal; magia: todas as direções).  
- Sem travamentos quando um jogador não tem ações válidas (pode encerrar).  
- Build roda com `yarn dev` e `yarn build`.  

## 15) Expansões pós-MVP (rápidas)

- Modos de vitória alternativos: controle de áreas por N turnos.  
- Magias com AoE 3x3 e linha reta.  
- Bloqueio de linha de visão (paredes/obstáculos).  
- Efeitos de status simples (ex.: “imobilizado 1 turno”).  
- Replay/seed para depuração.

## 16) Como orientar o Gemini CLI

- Prompts de geração por arquivo/módulo, com os critérios de aceitação como “tests to pass”.  
- Forçar determinismo (seed) no embaralhamento.  
- Pedir tests de unidade para: pagamento de energia, invocação válida/inválida, alcance de ataque, morte e vitória.  
