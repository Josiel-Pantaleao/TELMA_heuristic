# Agentes Inteligentes no NetLogo com Python Extension

Este repositório contém um modelo NetLogo que integra a lógica de decisão de um agente (usando Python) com a visualização e simulação do NetLogo. O modelo demonstra duas abordagens para a coleta de recursos em um ambiente:  
- **Agente Reativo Simples** (movimento aleatório)  
- **Agente com Objetivo** utilizando Busca em Largura (BFS)

Quando a capacidade do agente é atingida, ele retorna à posição inicial e muda de cor para vermelho. O modelo é ideal para entender conceitos básicos de agentes em Inteligência Artificial e as diferenças entre uma abordagem reativa e uma com planejamento.

## Pré-requisitos

- **NetLogo 6.x ou superior**  
- **Python 3** instalado no sistema  
- **Python Extension para NetLogo**  
  - Baixe a extensão [Python-Extension](https://github.com/NetLogo/Python-Extension) e copie os arquivos (por exemplo, `py.jar` e `pyext.py`) para a pasta `extensions/py` do NetLogo ou para a pasta de extensões do seu modelo.

## Configuração do Python no NetLogo

1. **Configurar o caminho do Python (opcional):**  
   - Você pode configurar o caminho para o seu executável do Python através do menu **Python > Configure** no NetLogo, ou editando o arquivo `python.properties` na pasta `extensions/py`.
   - Por exemplo, em sistemas Windows, o caminho pode ser algo como:
     ```
     python3=C:\Users\SeuUsuario\AppData\Local\Programs\Python\Python39\python.exe
     ```

## Instruções de Uso

### 1. Clone o Repositório

No terminal, execute:
```bash
git clone git@https://github.com/Josiel-Pantaleao/TELMA_heuristic.git
```

### 2. Abra o Modelo no NetLogo

- Inicie o NetLogo.
- Abra o arquivo do modelo (por exemplo, `AgentesInteligentes.nlogo`) presente no repositório.

### 3. Configure a Simulação

O modelo contém dois procedimentos principais: `setup` e `go`.

- **Setup:**  
  - O procedimento `setup` inicializa o ambiente, define os patches com recursos (com 20% de chance) e cria o personagem que representa o agente.
  - Ele também inicia a sessão Python, carrega o código Python (em uma única linha, usando `\n` para as quebras de linha (FIZ ISSO POIS ESTAVA DANDO UM ERRO INSUPORTÁVEL DE ASPAS) e envia os dados do ambiente para o Python.
  - **Importante:** Clique no botão **Setup** para inicializar tudo. No Command Center, você deverá ver uma lista de nomes (por exemplo, `"step_agent"` aparecerá na saída do `dir()`), o que confirma que o código Python foi carregado corretamente.

- **Go:**  
  - Em cada tick, o NetLogo chama a função Python `step_agent` para calcular o próximo movimento do agente.
  - O agente se move, coleta recursos (que são removidos visualmente), e, quando atingir a capacidade máxima e retornar à posição inicial, a tartaruga muda de cor para vermelho e a simulação para automaticamente.
  - Se não houver mais recursos no mundo, uma mensagem é exibida e a simulação é encerrada.

### 4. Rodando a Simulação

- **Passo 1:** Clique em **Setup**.  
- **Passo 2:** Clique em **Go**.

O agente se moverá automaticamente no ambiente, coletando recursos. Observe o comportamento:
- Em **modo BFS** (definido na variável `let mode "bfs"` do procedimento `go`), o agente buscará o caminho mais curto até o recurso mais próximo.
- Em **modo reativo simples** (caso você altere para `let mode "random"`), o agente se moverá de forma aleatória.

Quando o agente atingir sua capacidade e voltar à posição inicial, ele ficará vermelho e a simulação encerrará.

## Estrutura do Código

- **setup:** Inicializa patches, carrega o código Python e envia os dados do ambiente.
- **go:** Chama a função Python `step_agent` a cada tick para atualizar a posição do agente e verificar as condições de parada.

## Personalização

- **Capacidade do Agente:** Altere o valor passado para a função `init_environment_and_agent` (atualmente definido como `5`).
- **Probabilidade de Recurso:** Modifique `(random-float 1.0 < 0.2)` no procedimento `setup` para aumentar ou diminuir a quantidade de recursos.
- **Modo de Movimento:** Para testar o comportamento reativo simples, altere a variável `mode` no procedimento `go` para `"random"`.

## Possíveis Erros e Soluções

- **"closing double quote is missing":**  
  Certifique-se de que o código Python esteja em uma única linha com `\n` para as quebras de linha.  
- **"name 'step_agent' is not defined":**  
  Execute o `setup` para carregar o código Python antes de chamar o `go`.

## Referências

1. [NetLogo Official Website](http://ccl.northwestern.edu/netlogo/index.shtml)
2. [Python Extension for NetLogo GitHub](https://github.com/NetLogo/Python-Extension)
3. Recursos de Inteligência Artificial e Busca em Largura (BFS) conforme indicados na atividade.
4. Capítulo 3.4 do livro Stuart Russell e Peter Norvig. Inteligência Artificial - Tradução da
Terceira Edição. Elsevier Editora Ltda, 2013
5. Buscas em Largura e Profundidade aplicadas à Inteligência Artificial – IAsc – Inteligência
Artificial sob controle (wordpress.com) 
